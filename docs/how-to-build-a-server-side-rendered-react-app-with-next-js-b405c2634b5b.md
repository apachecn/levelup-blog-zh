# 如何用 Next.js 构建服务器端渲染的 React app

> 原文：<https://levelup.gitconnected.com/how-to-build-a-server-side-rendered-react-app-with-next-js-b405c2634b5b>

**现在在【http://jauyeung.net/subscribe/】[](http://jauyeung.net/subscribe/)****订阅我的邮件列表。******

****在推特上关注我**[**https://twitter.com/AuMayeung**](https://twitter.com/AuMayeung)**

**React 最受欢迎的代码生成器 Create React App 创建了一个客户端渲染的应用程序，这意味着加载您页面的每个人都可以下载整个应用程序，所有前端代码都在客户端运行。这意味着没有什么比运行 JavaScript 让网络爬虫索引页面更好的搜索引擎优化了。它也比客户端渲染慢，因为在客户端运行 JavaScript 不是很快。**

**使用 Create React App 生成的默认代码来设置服务器端呈现的应用程序并不容易。您必须对默认代码做大量的修改才能让任何东西工作。让它完全按照你想要的方式工作更加困难，所以开发人员想出了一些解决方案。最好的选择之一是 Next.js。**

**在这个故事中，我们将构建一个地址簿应用程序，它使用那些库，加上 React Bootstrap，它与上面的那些库有很大的集成，可以创建表单。首先，我们需要运行 Next.js CLI 来搭建应用程序。我们运行`npx create-next-app`来创建包含初始文件的应用项目文件夹。该应用程序将有一个主页来显示联系人，并让我们打开一个模式来添加联系人。将有一个表，显示所有的联系人和编辑和删除按钮，每一行编辑或删除每个联系人。联系人将存储在一个中央 Redux 存储中，以便将联系人存储在一个中央位置，使他们易于访问。React 路由器将用于路由。联系人将保存在使用 [JSON 服务器包](https://github.com/typicode/json-server)生成的后端中。**

**对于表单验证，则需要使用第三方库。 [Formik](https://github.com/jaredpalmer/formik) 和 [Yup](https://github.com/jquense/yup) 配合得非常好，让我们能够满足大多数表单验证需求。Formik 让我们构建表单，显示错误，并处理表单值的更改，这是另一件我们必须亲自完成的事情。是的，让我们写一个模式来验证我们的表单域。它可以检查几乎任何东西，像电子邮件和必填字段作为内置功能可用的通用验证码。它还可以检查依赖于其他字段的字段，比如依赖于国家的邮政编码格式。Bootstrap 表单可以无缝地与 Formik 和 Yup 一起使用。**

**一旦完成，我们必须安装一些库。为了安装我们上面提到的库，我们运行`npm i axios bootstrap formik react-bootstrap react-redux react-router-dom yup`。Axios 是我们用来向后端发出 HTTP 请求的 HTTP 客户端。`react-router-dom`是 React 路由器最新版本的包名。**

**现在我们已经安装了所有的库，我们可以开始构建应用程序了。我们创建一个`store`文件夹，并在其中创建一个名为`actionCreator.js`的文件，然后添加以下内容:**

```
import { SET_CONTACTS } from './actions';const setContacts = (contacts) => {
    return {
        type: SET_CONTACTS,
        payload: contacts
    }
};export { setContacts };
```

**这是动作创建器，用于创建在商店中存储联系人的动作。**

**我们在同一个文件夹中创建另一个名为`actions.js`的文件，并添加:**

```
const SET_CONTACTS = 'SET_CONTACTS';export { SET_CONTACTS };
```

**这只是调度动作的类型常量。**

**然后在`store`文件夹中，我们创建`index.js`并添加:**

```
import { contactsReducer } from "./reducers";
import { createStore, combineReducers } from "redux";const addressBookApp = combineReducers({
  contacts: contactsReducer,
});const makeStore = (initialState, options) => {
  return createStore(addressBookApp, initialState);
};export { makeStore };
```

**我们将在主入口点文件中使用它，该文件将在`pages`文件夹中被称为`_app.js`，以允许我们在这个多页面、服务器端呈现的应用程序中使用相同的 Redux 存储。**

**然后我们制作一个名为`reducers.js`的文件，并添加:**

```
import { SET_CONTACTS } from './actions';function contactsReducer(state = {}, action) {
    switch (action.type) {
        case SET_CONTACTS:
            state = JSON.parse(JSON.stringify(action.payload));
            return state;
        default:
            return state
    }
}export { contactsReducer };
```

**这是一个缩减器，我们通过调用组件中的`mapDispatchToProps`函数提供的属性来存储我们发送的联系人。**

**接下来，我们向`pages`文件夹添加一些代码文件。**

**在`index.js`中，我们用以下内容替换现有内容:**

```
import React from "react";
import Head from "next/head";
import { Router, Route } from "react-router-dom";
import { createMemoryHistory as createHistory } from "history";
import Navbar from "react-bootstrap/Navbar";
import Nav from "react-bootstrap/Nav";
import HomePage from "./HomePage";
import { contactsReducer } from "../store/reducers";
import { Provider } from "react-redux";
import { createStore, combineReducers } from "redux";const history = createHistory();const addressBookApp = combineReducers({
  contacts: contactsReducer,
});const store = createStore(addressBookApp);const Home = () => (
  <div>
    <Head>
      <title>Address Book</title>
      <link
        href="[https://maxcdn.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css](https://maxcdn.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css)"
        rel="stylesheet"
        integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T"
        crossOrigin="anonymous"
      />
    </Head>
    <div className="App">
      <Router history={history}>
        <Navbar bg="primary" expand="lg" variant="dark">
          <Navbar.Brand href="#home">Address Book App</Navbar.Brand>
          <Navbar.Toggle aria-controls="basic-navbar-nav" />
          <Navbar.Collapse id="basic-navbar-nav">
            <Nav className="mr-auto">
              <Nav.Link href="/">Home</Nav.Link>
            </Nav>
          </Navbar.Collapse>
        </Navbar>
        <Route path="/" exact component={HomePage} />
      </Router>
    </div> <style jsx>{`
      .App {
        text-align: center;
      }
    `}</style>
  </div>
);export default Home;
```

**这是我们添加导航栏并显示 React 路由器路由的路线的地方。在`styles`元素中，我们将现有代码替换为:**

```
.App {
  text-align: center;
}
```

**将一些文本居中。**

**接下来，我们建立我们的联系形式。这是我们的应用程序中逻辑最强的部分。我们在`components`文件夹中创建一个名为`ContactForm.js`的文件，并添加:**

```
import React from 'react';
import { Formik } from 'formik';
import Form from 'react-bootstrap/Form';
import Col from 'react-bootstrap/Col';
import InputGroup from 'react-bootstrap/InputGroup';
import Button from 'react-bootstrap/Button';
import * as yup from 'yup';
import { COUNTRIES } from '../helpers/exports';
import PropTypes from 'prop-types';
import { addContact, editContact, getContacts } from '../helpers/requests';
import { connect } from 'react-redux';
import { setContacts } from '../store/actionCreators';const schema = yup.object({
  firstName: yup.string().required('First name is required'),
  lastName: yup.string().required('Last name is required'),
  address: yup.string().required('Address is required'),
  city: yup.string().required('City is required'),
  region: yup.string().required('Region is required'),
  country: yup.string().required('Country is required').default('Afghanistan'),
  postalCode: yup
    .string()
    .when('country', {
      is: 'United States',
      then: yup.string().matches(/^[0-9]{5}(?:-[0-9]{4})?$/, 'Invalid postal code'),
    })
    .when('country', {
      is: 'Canada',
      then: yup.string().matches(/^[A-Za-z]\d[A-Za-z][ -]?\d[A-Za-z]\d$/, 'Invalid postal code'),
    })
    .required(),
  phone: yup
    .string()
    .when('country', {
      is: country => ["United States", "Canada"].includes(country),
      then: yup.string().matches(/^[2-9]\d{2}[2-9]\d{2}\d{4}$/, 'Invalid phone nunber')
    })
    .required(),
  email: yup.string().email('Invalid email').required('Email is required'),
  age: yup.number()
    .required('Age is required')
    .min(0, 'Minimum age is 0')
    .max(200, 'Maximum age is 200'),
});function ContactForm({
  edit,
  onSave,
  setContacts,
  contact,
  onCancelAdd,
  onCancelEdit,
}) {
  const handleSubmit = async (evt) => {
    const isValid = await schema.validate(evt);
    if (!isValid) {
      return;
    }
    if (!edit) {
      await addContact(evt);
    }
    else {
      await editContact(evt);
    }
    const response = await getContacts();
    setContacts(response.data);
    onSave();
  }return (
    <div className="form">
      <Formik
        validationSchema={schema}
        onSubmit={handleSubmit}
        initialValues={contact || {}}
      >
        {({
          handleSubmit,
          handleChange,
          handleBlur,
          values,
          touched,
          isInvalid,
          errors,
        }) => (
            <Form noValidate onSubmit={handleSubmit}>
              <Form.Row>
                <Form.Group as={Col} md="12" controlId="firstName">
                  <Form.Label>First name</Form.Label>
                  <Form.Control
                    type="text"
                    name="firstName"
                    placeholder="First Name"
                    value={values.firstName || ''}
                    onChange={handleChange}
                    isInvalid={touched.firstName && errors.firstName}
                  />
                  <Form.Control.Feedback type="invalid">
                    {errors.firstName}
                  </Form.Control.Feedback>
                </Form.Group>
                <Form.Group as={Col} md="12" controlId="lastName">
                  <Form.Label>Last name</Form.Label>
                  <Form.Control
                    type="text"
                    name="lastName"
                    placeholder="Last Name"
                    value={values.lastName || ''}
                    onChange={handleChange}
                    isInvalid={touched.firstName && errors.lastName}
                  /><Form.Control.Feedback type="invalid">
                    {errors.lastName}
                  </Form.Control.Feedback>
                </Form.Group>
                <Form.Group as={Col} md="12" controlId="address">
                  <Form.Label>Address</Form.Label>
                  <InputGroup>
                    <Form.Control
                      type="text"
                      placeholder="Address"
                      aria-describedby="inputGroupPrepend"
                      name="address"
                      value={values.address || ''}
                      onChange={handleChange}
                      isInvalid={touched.address && errors.address}
                    />
                    <Form.Control.Feedback type="invalid">
                      {errors.address}
                    </Form.Control.Feedback>
                  </InputGroup>
                </Form.Group>
              </Form.Row>
              <Form.Row>
                <Form.Group as={Col} md="12" controlId="city">
                  <Form.Label>City</Form.Label>
                  <Form.Control
                    type="text"
                    placeholder="City"
                    name="city"
                    value={values.city || ''}
                    onChange={handleChange}
                    isInvalid={touched.city && errors.city}
                  /><Form.Control.Feedback type="invalid">
                    {errors.city}
                  </Form.Control.Feedback>
                </Form.Group>
                <Form.Group as={Col} md="12" controlId="region">
                  <Form.Label>Region</Form.Label>
                  <Form.Control
                    type="text"
                    placeholder="Region"
                    name="region"
                    value={values.region || ''}
                    onChange={handleChange}
                    isInvalid={touched.region && errors.region}
                  />
                  <Form.Control.Feedback type="invalid">
                    {errors.region}
                  </Form.Control.Feedback>
                </Form.Group><Form.Group as={Col} md="12" controlId="country">
                  <Form.Label>Country</Form.Label>
                  <Form.Control
                    as="select"
                    placeholder="Country"
                    name="country"
                    onChange={handleChange}
                    value={values.country || ''}
                    isInvalid={touched.region && errors.country}>
                    {COUNTRIES.map(c => <option key={c} value={c}>{c}</option>)}
                  </Form.Control>
                  <Form.Control.Feedback type="invalid">
                    {errors.country}
                  </Form.Control.Feedback>
                </Form.Group><Form.Group as={Col} md="12" controlId="postalCode">
                  <Form.Label>Postal Code</Form.Label>
                  <Form.Control
                    type="text"
                    placeholder="Postal Code"
                    name="postalCode"
                    value={values.postalCode || ''}
                    onChange={handleChange}
                    isInvalid={touched.postalCode && errors.postalCode}
                  /><Form.Control.Feedback type="invalid">
                    {errors.postalCode}
                  </Form.Control.Feedback>
                </Form.Group><Form.Group as={Col} md="12" controlId="phone">
                  <Form.Label>Phone</Form.Label>
                  <Form.Control
                    type="text"
                    placeholder="Phone"
                    name="phone"
                    value={values.phone || ''}
                    onChange={handleChange}
                    isInvalid={touched.phone && errors.phone}
                  /><Form.Control.Feedback type="invalid">
                    {errors.phone}
                  </Form.Control.Feedback>
                </Form.Group><Form.Group as={Col} md="12" controlId="email">
                  <Form.Label>Email</Form.Label>
                  <Form.Control
                    type="text"
                    placeholder="Email"
                    name="email"
                    value={values.email || ''}
                    onChange={handleChange}
                    isInvalid={touched.email && errors.email}
                  /><Form.Control.Feedback type="invalid">
                    {errors.email}
                  </Form.Control.Feedback>
                </Form.Group><Form.Group as={Col} md="12" controlId="age">
                  <Form.Label>Age</Form.Label>
                  <Form.Control
                    type="text"
                    placeholder="Age"
                    name="age"
                    value={values.age || ''}
                    onChange={handleChange}
                    isInvalid={touched.age && errors.age}
                  /><Form.Control.Feedback type="invalid">
                    {errors.age}
                  </Form.Control.Feedback>
                </Form.Group>
              </Form.Row>
              <Button type="submit" style={{ 'marginRight': '10px' }}>Save</Button>
              <Button type="button" onClick={edit ? onCancelEdit : onCancelAdd}>Cancel</Button>
            </Form>
          )}
      </Formik>
    </div>
  );
}ContactForm.propTypes = {
  edit: PropTypes.bool,
  onSave: PropTypes.func,
  onCancelAdd: PropTypes.func,
  onCancelEdit: PropTypes.func,
  contact: PropTypes.object
}const mapStateToProps = state => {
  return {
    contacts: state.contacts,
  }
}const mapDispatchToProps = dispatch => ({
  setContacts: contacts => dispatch(setContacts(contacts))
})export default connect(
  mapStateToProps,
  mapDispatchToProps
)(ContactForm);
```

**我们使用 Formik 来帮助构建我们的联系表单，我们的 Boostrap `Form`组件嵌套在`Formik`组件中，这样我们就可以使用 Formik 的`handleChange`、`handleSubmit`、`values`、`touched`和`errors`参数。`handleChange`是一个函数，让我们从输入中更新表单域数据，而无需我们自己编写代码。`handleSubmit`是我们传递给`Formik`组件的`onSubmit`处理程序的函数。函数中的参数是我们输入的数据，字段名作为键，由每个字段的`name`属性定义，每个字段的值作为那些键的值。注意，在每个`value`属性中，我们有`||''`，这样我们就不会得到未定义的值，并防止触发不受控制的表单警告。**

**为了显示表单验证消息，我们必须将`isInvalid`属性传递给每个`Form.Control`组件。`schema`对象是`Formik`将检查表单验证的对象。`required`函数中的参数是验证错误消息。`matches`、`min`和`max`功能的第二个参数也是验证消息。**

**`ContactForm`函数的参数是道具，我们将从稍后构建的`HomePage`组件传入。`handleSubmit`功能检查数据是否有效，如果有效，则根据是添加还是编辑联系人进行保存。然后，当保存成功时，我们在存储中设置联系人并调用`onSave` prop，这是一个关闭表单所在模态的函数。模式将在主页中定义。**

**`mapStateToProps`是 React Redux 提供的一个函数，这样我们就可以如函数名所示将状态直接映射到组件的道具上。`mapDispatchToProps`允许我们调用名为`setContacts`的组件的 props 中的函数来调度我们在`actionCreators.js`中定义的动作。**

**接下来，在创建了`helpers`文件夹之后，我们创建一个名为`exports.js`的文件，并放入:**

```
export const COUNTRIES = [
  "Afghanistan",
  "Albania",
  "Algeria",
  "Andorra",
  "Angola",
  "Anguilla",
  "Antigua &amp; Barbuda",
  "Argentina",
  "Armenia",
  "Aruba",
  "Australia",
  "Austria",
  "Azerbaijan",
  "Bahamas",
  "Bahrain",
  "Bangladesh",
  "Barbados",
  "Belarus",
  "Belgium",
  "Belize",
  "Benin",
  "Bermuda",
  "Bhutan",
  "Bolivia",
  "Bosnia &amp; Herzegovina",
  "Botswana",
  "Brazil",
  "British Virgin Islands",
  "Brunei",
  "Bulgaria",
  "Burkina Faso",
  "Burundi",
  "Cambodia",
  "Cameroon",
  "Canada",
  "Cape Verde",
  "Cayman Islands",
  "Chad",
  "Chile",
  "China",
  "Colombia",
  "Congo",
  "Cook Islands",
  "Costa Rica",
  "Cote D Ivoire",
  "Croatia",
  "Cruise Ship",
  "Cuba",
  "Cyprus",
  "Czech Republic",
  "Denmark",
  "Djibouti",
  "Dominica",
  "Dominican Republic",
  "Ecuador",
  "Egypt",
  "El Salvador",
  "Equatorial Guinea",
  "Estonia",
  "Ethiopia",
  "Falkland Islands",
  "Faroe Islands",
  "Fiji",
  "Finland",
  "France",
  "French Polynesia",
  "French West Indies",
  "Gabon",
  "Gambia",
  "Georgia",
  "Germany",
  "Ghana",
  "Gibraltar",
  "Greece",
  "Greenland",
  "Grenada",
  "Guam",
  "Guatemala",
  "Guernsey",
  "Guinea",
  "Guinea Bissau",
  "Guyana",
  "Haiti",
  "Honduras",
  "Hong Kong",
  "Hungary",
  "Iceland",
  "India",
  "Indonesia",
  "Iran",
  "Iraq",
  "Ireland",
  "Isle of Man",
  "Israel",
  "Italy",
  "Jamaica",
  "Japan",
  "Jersey",
  "Jordan",
  "Kazakhstan",
  "Kenya",
  "Kuwait",
  "Kyrgyz Republic",
  "Laos",
  "Latvia",
  "Lebanon",
  "Lesotho",
  "Liberia",
  "Libya",
  "Liechtenstein",
  "Lithuania",
  "Luxembourg",
  "Macau",
  "Macedonia",
  "Madagascar",
  "Malawi",
  "Malaysia",
  "Maldives",
  "Mali",
  "Malta",
  "Mauritania",
  "Mauritius",
  "Mexico",
  "Moldova",
  "Monaco",
  "Mongolia",
  "Montenegro",
  "Montserrat",
  "Morocco",
  "Mozambique",
  "Namibia",
  "Nepal",
  "Netherlands",
  "Netherlands Antilles",
  "New Caledonia",
  "New Zealand",
  "Nicaragua",
  "Niger",
  "Nigeria",
  "Norway",
  "Oman",
  "Pakistan",
  "Palestine",
  "Panama",
  "Papua New Guinea",
  "Paraguay",
  "Peru",
  "Philippines",
  "Poland",
  "Portugal",
  "Puerto Rico",
  "Qatar",
  "Reunion",
  "Romania",
  "Russia",
  "Rwanda",
  "Saint Pierre &amp; Miquelon",
  "Samoa",
  "San Marino",
  "Satellite",
  "Saudi Arabia",
  "Senegal",
  "Serbia",
  "Seychelles",
  "Sierra Leone",
  "Singapore",
  "Slovakia",
  "Slovenia",
  "South Africa",
  "South Korea",
  "Spain",
  "Sri Lanka",
  "St Kitts &amp; Nevis",
  "St Lucia",
  "St Vincent",
  "St. Lucia",
  "Sudan",
  "Suriname",
  "Swaziland",
  "Sweden",
  "Switzerland",
  "Syria",
  "Taiwan",
  "Tajikistan",
  "Tanzania",
  "Thailand",
  "Timor L'Este",
  "Togo",
  "Tonga",
  "Trinidad &amp; Tobago",
  "Tunisia",
  "Turkey",
  "Turkmenistan",
  "Turks &amp; Caicos",
  "Uganda",
  "Ukraine",
  "United Arab Emirates",
  "United Kingdom",
  "United States",
  "United States Minor Outlying Islands",
  "Uruguay",
  "Uzbekistan",
  "Venezuela",
  "Vietnam",
  "Virgin Islands (US)",
  "Yemen",
  "Zambia",
  "Zimbabwe",
];
```

**这些是表单中国家字段的国家。**

**然后，我们在同一个文件夹中创建一个名为`requests.js`的文件，并添加:**

```
const APIURL = '[http://localhost:3000'](http://localhost:3000');
const axios = require('axios');export const getContacts = () => axios.get(`${APIURL}/contacts`);export const addContact = (data) => axios.post(`${APIURL}/contacts`, data);export const editContact = (data) => axios.put(`${APIURL}/contacts/${data.id}`, data);export const deleteContact = (id) => axios.delete(`${APIURL}/contacts/${id}`);
```

**这些函数向后端发出 HTTP 请求，以保存和删除联系人。**

**在`HomePage.js`中，我们放入:**

```
import React from 'react';
import { useState, useEffect } from 'react';
import Table from 'react-bootstrap/Table'
import ButtonToolbar from 'react-bootstrap/ButtonToolbar';
import Button from 'react-bootstrap/Button';
import Modal from 'react-bootstrap/Modal'
import ContactForm from './ContactForm';
import './HomePage.css';
import { connect } from 'react-redux';
import { getContacts, deleteContact } from './requests';function HomePage() {
  const [openAddModal, setOpenAddModal] = useState(false);
  const [openEditModal, setOpenEditModal] = useState(false);
  const [initialized, setInitialized] = useState(false);
  const [selectedId, setSelectedId] = useState(0);
  const [selectedContact, setSelectedContact] = useState({});
  const [contacts, setContacts] = useState([]); const openModal = () => {
    setOpenAddModal(true);
  } const closeModal = () => {
    setOpenAddModal(false);
    setOpenEditModal(false);
    getData();
  } const cancelAddModal = () => {
    setOpenAddModal(false);
  } const editContact = (contact) => {
    setSelectedContact(contact);
    setOpenEditModal(true);
  } const cancelEditModal = () => {
    setOpenEditModal(false);
  } const getData = async () => {
    const response = await getContacts();
    setContacts(response.data);
    setInitialized(true);
  } const deleteSelectedContact = async (id) => {
    await deleteContact(id);
    getData();
  } useEffect(() => {
    if (!initialized) {
      getData();
    }
  }) return (
    <div className="home-page">
      <h1>Contacts</h1>
      <Modal show={openAddModal} onHide={closeModal} >
        <Modal.Header closeButton>
          <Modal.Title>Add Contact</Modal.Title>
        </Modal.Header>
        <Modal.Body>
          <ContactForm edit={false} onSave={closeModal.bind(this)} onCancelAdd={cancelAddModal} />
        </Modal.Body>
      </Modal><Modal show={openEditModal} onHide={closeModal}>
        <Modal.Header closeButton>
          <Modal.Title>Edit Contact</Modal.Title>
        </Modal.Header>
        <Modal.Body>
          <ContactForm edit={true} onSave={closeModal.bind(this)} contact={selectedContact} onCancelEdit={cancelEditModal} />
        </Modal.Body>
      </Modal>
      <ButtonToolbar onClick={openModal}>
        <Button variant="outline-primary">Add Contact</Button>
      </ButtonToolbar>
      <br />
      <Table striped bordered hover>
        <thead>
          <tr>
            <th>First Name</th>
            <th>Last Name</th>
            <th>Address</th>
            <th>City</th>
            <th>Country</th>
            <th>Postal Code</th>
            <th>Phone</th>
            <th>Email</th>
            <th>Age</th>
            <th>Edit</th>
            <th>Delete</th>
          </tr>
        </thead>
        <tbody>
          {contacts.map(c => (
            <tr key={c.id}>
              <td>{c.firstName}</td>
              <td>{c.lastName}</td>
              <td>{c.address}</td>
              <td>{c.city}</td>
              <td>{c.country}</td>
              <td>{c.postalCode}</td>
              <td>{c.phone}</td>
              <td>{c.email}</td>
              <td>{c.age}</td>
              <td>
                <Button variant="outline-primary" onClick={editContact.bind(this, c)}>Edit</Button>
              </td>
              <td>
                <Button variant="outline-primary" onClick={deleteSelectedContact.bind(this, c.id)}>Delete</Button>
              </td>
            </tr>
          ))}
        </tbody>
      </Table>
    </div>
  );
}const mapStateToProps = state => {
  return {
    contacts: state.contacts,
  }
}export default connect(
  mapStateToProps,
  null
)(HomePage);
```

**它有显示联系人的表格和添加、编辑和删除联系人的按钮。它在第一次加载时用`useEffect`的回调函数中的`getData`函数调用获取数据。每次渲染都会调用`useEffect`的回调，所以我们想要设置一个`initialized`标志，并检查它是否只在`true`时才加载。**

**注意，我们将这个组件中的所有道具传递给了`ContactForm`组件。要将参数传递给`onClick`处理函数，我们必须调用函数上的`bind`，并将函数的参数作为第二个参数传递给`bind`。例如，在这个文件中，我们有`editContact.bind(this, c)`，其中`c`是联系对象。`editContact`功能定义如下:**

```
const editContact = (contact) => {
    setSelectedContact(contact);
    setOpenEditModal(true);
  }
```

**`c`是我们传入的`contact`参数。**

**在`styles`模块中，我们有:**

```
.home-page {
  padding: 20px;
}
```

**添加一些填充。**

**在`pages`文件夹的`index.js`中，我们将现有代码替换为:**

```
import React from "react";
import Head from "next/head";
import { Router, Route } from "react-router-dom";
import { createMemoryHistory as createHistory } from "history";
import Navbar from "react-bootstrap/Navbar";
import Nav from "react-bootstrap/Nav";
import HomePage from "./HomePage";
import { contactsReducer } from "../store/reducers";
import { Provider } from "react-redux";
import { createStore, combineReducers } from "redux";const history = createHistory();const addressBookApp = combineReducers({
  contacts: contactsReducer,
});const store = createStore(addressBookApp);const Home = () => (
  <div>
    <Head>
      <title>Address Book</title>
      <link
        href="[https://maxcdn.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css](https://maxcdn.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css)"
        rel="stylesheet"
        integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T"
        crossOrigin="anonymous"
      />
    </Head>
    <div className="App">
      <Router history={history}>
        <Navbar bg="primary" expand="lg" variant="dark">
          <Navbar.Brand href="#home">Address Book App</Navbar.Brand>
          <Navbar.Toggle aria-controls="basic-navbar-nav" />
          <Navbar.Collapse id="basic-navbar-nav">
            <Nav className="mr-auto">
              <Nav.Link href="/">Home</Nav.Link>
            </Nav>
          </Navbar.Collapse>
        </Navbar>
        <Route path="/" exact component={HomePage} />
      </Router>
    </div> <style jsx>{`
      .App {
        text-align: center;
      }
    `}</style>
  </div>
);export default Home;
```

**这是应用程序的入口点，我们在这里添加导航菜单，也在这里添加主页的路径。由于我们在服务器端呈现的应用程序中没有`index.html`，我们通过将`Head`组件放在这里来呈现页面的`head`标签，同时将`title`和`link`组件放在`Head`中。我们包含这些分别是为了更改标题和添加引导样式表。**

**我们必须在`pages`文件夹中添加一个名为`_app.js`的文件，让我们在所有组件中使用 Redux 存储，因为这不是一个普通的客户端渲染应用程序。这个文件覆盖了 Next.js 中默认的`App`类。该类用于在页面中加载初始化代码。没有对最顶层组件的`ReactDOM.render`调用，我们可以将`Provider`组件包装在它周围，让我们可以在任何地方使用我们的 Redux 存储，所以我们必须添加:**

```
// pages/_app.js
import React from "react";
import { Provider } from "react-redux";
import App, { Container } from "next/app";
import withRedux from "next-redux-wrapper";
import { contactsReducer } from "../store/reducers";
import { createStore, combineReducers } from "redux";const addressBookApp = combineReducers({
  contacts: contactsReducer,
});const makeStore = (initialState, options) => {
  return createStore(addressBookApp, initialState);
};class MyApp extends App {
  static async getInitialProps({ Component, ctx }) {
    const pageProps = Component.getInitialProps
      ? await Component.getInitialProps(ctx)
      : {}; return { pageProps };
  } render() {
    const { Component, pageProps, store } = this.props;
    return (
      <Container>
        <Provider store={store}>
          <Component {...pageProps} />
        </Provider>
      </Container>
    );
  }
}export default withRedux(makeStore)(MyApp);
```

**将我们的 Redux 存储包在所有组件周围。`Component`是我们应用中的任何组件。我们使用`next-redux-wrapper`包将`store`对象传递给我们所有的组件，允许我们用`store`道具将`Provider`包裹在我们的组件周围。**

**现在，我们可以通过运行`npm run build`然后运行`npm run start -- --port 3001`来运行应用程序。**

**为了启动后端，我们首先通过运行`npm i json-server`来安装`json-server`包。然后转到我们的项目文件夹并运行:**

```
json-server --watch db.json
```

**在`db.json`中，将文本改为:**

```
{
  "contacts": [
  ]
}
```

**这样我们就有了在`requests.js`中定义的`contacts`端点。**

**最后，我们有以下内容:**

**![](img/f0189119955e2e23d8ca9a28cc9761f9.png)****![](img/751d2681035b39a9bbd8da8b261ec55b.png)****![](img/9d3348846e2374867d8616963dcd66e0.png)**