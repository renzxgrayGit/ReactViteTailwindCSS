# React + Vite + Tailwind CSS

npm install react-router-dom axios bootstrap json-server

create db.json and put json data inside. You may put ID, NAME, USERNAME, EMAIL, PHONE, WEBSITE for sample.

create JSX components in src folder: Home, Create, Read and Update and put rafce each component.

go to App.jsx and put all components in BrowserRouter > Routes > Route and import these from react-router-dom, inside Route element put path="" and element="".

inside terminal type: json-server --watch db.json and install this: npm install -g json-server if ever you'll have problem to run it.

GO to Home.jsx to display your db.json, to do that: CHECK FIRST in CONSOLE your object db.json:
useEffect(() => {})
axios.get('http://localhost:3000/users') , users = name of your json data in db.json
.then(res => console.log(res))
.catch(err => console.log(err))
and dont forget the [] for DEPENDENCY of useEffect, to run it once.

If your data showed in your Console, put your data object in Variable State.

create useState to put your data on variable, [data, setData] = useState([]) , the [] or square bracket represents as an empty array, meaning that 'data' starts off as an empty array.

change your .then INTO .then(res => setData(res.data)) to pass the data id, name, username etc.. and display it in your jsx

create table > thead > tr > th = ID, NAME, EMAIL, PHONE, ACTION and
tbody > data.map((data, index) => ( tr key={index} > td = {data.ID},{data.name},{data.email}))

add 3 buttons for Read, Edit, Delete inside td or table data

add div > Link to="/create" > Add User, import Link from react-router-dom

GO to Create.jsx and create Add user consists of Name, Email, Phone
create div > h1 Add User > form > div > label htmlFor="name" > input name="name" (as well as for Email and Phone) > button Submit > Link Back to Home.jsx

create useState to put Add User on variable, [values, setValues] = useState({name:'', email:'', phone:''})

add onChange={e => setValues({...values, name: e.target.value})} , for every INPUT name, email and phone. CHANGE THE PROPERTIES FOR NAME, EMAIL, PHONE!

add onSubmit={handleSubmit} in form,

create FUNCTION for handleSubmit = (event) => {}
event.preventDefault();
axios.post('http://localhost:3000/users', values) , we use POST bcz we're adding new user, and ADD the STATE values in link
.then(res => {console.log(res) navigate('/')}) , CREATE navigate = useNavigate(); to use useNavigate you need to import to react-router-dom.
.catch(err => console.log(err))

MAKE SURE TO IMPORT WHAT MUST TO IMPORT!
import axios from 'axios';
import React, { useEffect, useState } from 'react'
import { Link, useNavigate, useParams } from 'react-router-dom'

GO to Home.jsx CHANGE button Read to Link to={`/read/${data.id}`}

GO to Read.jsx and add below: (You can copy some codes in Home.jsx and add id to pass paramater)
const [data, setData] = useState([])
const {id} = useParams();
useEffect(() => {
axios.get('http://localhost:3000/users/'+ id)
.then(res => setData(res.data))
.catch(err => console.log(err))
}, [])

(make sure this is correct axios.get('http://localhost:3000/users/'+ id))

create div > h3 Detail of User > div > p Name: {data.name, data.email and phone} > Link to={`/update/${id}`} Edit > Link to="/" Back

GO to Update.jsx and create Update user consists of Name, Email, Phone
create div > h1 Update User > form > div > label htmlFor="name" > input name="name" (as well as for Email and Phone) > button Update > Link Back to Home.jsx (You can copy this in Create.jsx)

add below: (You can copy some codes in Read.jsx)
const [data, setData] = useState([])
const {id} = useParams();
useEffect(() => {
axios.get('http://localhost:3000/users/'+ id)
.then(res => setData(res.data))
.catch(err => console.log(err))
}, [])

add value={data.name},email and phone properties in INPUT element

TRY TO REMOVE onSubmit={handleSubmit} in FORM ELEMENT to check if its display the data.name, email, phone in Input element

create useState to put Add User on variable, [values, setValues] = useState({name:'', email:'', phone:''}) (You can copy this in Create.jsx)

add onSubmit={handleUpdate} in FORM ELEMENT

create a FUNCTION handleUpdate = (event) => {} (You can copy some codes in Create.jsx)
event.preventDefault();
axios.put('http://localhost:3000/users/' + id, values) , we use PUT bcz we're UPDATING user, ADD the id, and ADD the STATE values in link
.then(res => {console.log(res) navigate('/')}) , CREATE navigate = useNavigate(); to use useNavigate you need to import to react-router-dom.
.catch(err => console.log(err))

UPDATE your .then inside useEffect
useEffect(() => {
axios.get('http://localhost:3000/users/'+ id)
.then(res => setValues(res.data)) <-------------
.catch(err => console.log(err))
}, [])

change value={values.name},email and phone properties in INPUT element

GO to Home.jsx CHANGE button Edit to Link to={`/update/${data.id}`}

add onClick={e => handleDelete(data.id)} in button DELETE

create FUNCTION handleDelete:
handleDelete = (id) => {}
const confirmDelete = window.confirm("Would you like to Delete?");
if (confirmDelete) {}
axios.delete(`http://localhost:3000/users/${id}`)
.then(() => {  
setData(data.filter(user => user.id !== id)); Update the state after deleting
})
.catch(err => console.log(err));
