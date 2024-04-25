# coderest
import React, { useState,useEffect } from 'react'
import axios from 'axios'
import { useNavigate } from 'react-router-dom'

function Rest() {
    let navigate=useNavigate()
    const[restarray,setrestarray]=useState([])
    function click(e,id,type){
        if(type==="delete"){
            window.confirm("Are you sure you want to delete this data")
            axios.delete(`http://localhost:8000/data/${id}`).then((data)=>{
                console.log("data deleted succeessfully")
                
              }).catch(((error)=>{
                console.log("delete api failed")
                console.log(error)
              }))
              //window.location.reload()
        }
        else{
            navigate(`/form/${id}`)

        }


    }
    
  useEffect(()=>{
    (()=>{
      axios.get(`http://localhost:8000/data`).then((data)=>{
        console.log("data fetched succeessfully")
        setrestarray(data.data)
        
      }).catch(((error)=>{
        console.log("fetch api failed")
        console.log(error)
      }))
    })()



  },[restarray])
  function add(){
    navigate("/forma")
  }
  return (
    
    <center>
    <h1>Api records</h1>
    <table>
    <tr>
<th>sr. no. </th>
<th>Name</th>
<th>Contact</th>
<th>Email</th>
<th>Address</th>
<th>Profile picture</th>
<th>Edit</th>
<th>Delete</th>
</tr>
{ restarray.length>0 ? restarray.map((ele,index)=>{
          return(
            <>
            <tr>
            <td>{index+1}</td>
            <td>{ele.name}</td>
            <td>{ele.contact}</td>
            <td>{ele.email}</td>
            <td>{ele.address}</td>
            <td><img style={{width:"100%",height:"100%"}} src={ele.img} alt='img not found'/></td>
            <td><button onClick={(e)=>{
             click(e,ele.id,"update")
            }} >update</button></td>
            <td><button  onClick={(e)=>{
              click(e,ele.id,"delete")
            }}>Delete</button></td>
        </tr>

            </>
          )
        })
        
         : <h1>Loading...</h1>

        }




</table>
<button onClick={add} className='add'>Add data</button>
</center>
  )
}

export default Rest
Form
import React, { useState } from 'react'
import { useNavigate, useParams } from 'react-router-dom'
import axios from 'axios'

function Form() {
    let {id}= useParams()
    let navigate=useNavigate()
    let[obj,setobj] =useState({
        name:"",
    contact:"",
    email:"",
    address:"",
    img:""

    })
    function change(e){
        let{name,value}= e.target
        setobj((pre)=>{
            return {...pre,[name]:value}
        })





    }
    function next(){
        axios.patch(`http://localhost:8000/data/${id}`,obj).then((data)=>{
            window.location.reload()
            console.log("data updated successfully")
            console.log(data.data)

        }).catch((err)=>console.log("patch api failed",err))
        setobj({
            name:"",
    contact:"",
    email:"",
    address:"",
    img:""
     } )
     navigate("/")


    }
    function back(){
        navigate("/")
       }
  return (
     
    <div id="one">
        <h2 id="one1">Physical details</h2>
        
        <p id="one2">Name</p> <input type="text" id="to14" name='name' onChange={change}/>
        
        <p id="one3">Contact</p> <input type="text" id="to15" name='contact' onChange={change}/>
        
        <p id="one4">Email</p> <input type="email" id="to16" name='email' onChange={change}/>
        
        <p id="one5">Address</p> <input type="text" id="to17" name='address' onChange={change}/>
        
        <p id="one6">Profile pic</p> <input type="file" id="to18" name='img' onChange={change}/>
        
        <button onClick={back} id="to19">back</button>

        <button onClick={next} id="to20">save</button>
        
        </div>
      
  )
}

export default Form
form 2
import React, { useState } from 'react'
import axios from 'axios'
import { useNavigate } from 'react-router-dom'

function Form2() {
    let navigate=useNavigate()
    let[obj,setobj] =useState({
        name:"",
    contact:"",
    email:"",
    address:"",
    img:""

    })
    function change(e){
        let{name,value}= e.target
        setobj((pre)=>{
            return {...pre,[name]:value}
        })




    }
    function Next(){
        axios.post(`http://localhost:8000/data`,obj).then((data)=>{
            window.location.reload()
            console.log("data added successfully")

        }).catch((err)=>console.log("post api failed",err))
        setobj({
            name:"",
    contact:"",
    email:"",
    address:"",
    img:""
     } )
     navigate("/")


    }
    function back(){
     navigate("/")
    }
  return (
     
    <div id="one">
        <h2 id="one1">Physical details</h2>
        
        <p id="one2">Name</p> <input type="text" id="to14" name='name' onChange={change}/>
        
        <p id="one3">Contact</p> <input type="text" id="to15" name='contact' onChange={change}/>
        
        <p id="one4">Email</p> <input type="email" id="to16" name='email' onChange={change}/>
        
        <p id="one5">Address</p> <input type="text" id="to17" name='address' onChange={change}/>
        
        <p id="one6">Profile pic</p> <input type="file" id="to18" name='img' onChange={change}/>
        
        <button onClick={back} id="to19">back</button>

        <button onClick={Next} id="to20">save</button>
        
        </div>
      
  )
}

export default Form2
index.js

#one
{

    border:2px solid red;
    height:550px;
    width:500px;
    margin-top:100px;
    margin-left:500px;
    background: url('./images/500x700.jpg');
    display:block


}

#one1 {
    margin-top: 45px;
    margin-left: 153px;
    color: yellow;
    
}



#one2 {
    margin-top: 45px;
    margin-left: 71px;
    color: yellow;
    font-size: 20px;
}

#to1 {
    margin-top: -47px;
    margin-left: 153px;
    position: absolute;
    height: 30px;
    width: 270px;
}

#one3 {
    margin-top: 45px;
    margin-left: 71px;
    color: yellow;
    font-size: 20px;
}

#to2 {
    margin-top: -47px;
    margin-left: 153px;
    position: absolute;
    height: 30px;
    width: 270px;
}

#one4 {
    margin-top: 45px;
    margin-left: 71px;
    color: yellow;
    font-size: 20px;
}

#to3 {
    margin-top: -47px;
    margin-left: 153px;
    position: absolute;
    height: 30px;
    width: 270px;
}

#one5 {
    margin-top: 45px;
    margin-left: 71px;
    color: yellow;
    font-size: 20px;
}

#to4 {
    margin-top: -47px;
    margin-left: 153px;
    position: absolute;
    height: 30px;
    width: 270px;
}

#one6 {
    margin-top: 45px;
    margin-left: 71px;
    color: yellow;
    font-size: 20px;
}

#to5 {
    margin-top: -47px;
    margin-left: 153px;
    position: absolute;
    height: 30px;
    width: 270px;
}

#to6 {
    margin-top: 39px;
    margin-left: 230px;
}
table,td,th
{
border:1px solid white;
border-collapse:collapse;
width:800px;
height:100px;
text-align:center;
background-color:green;
color: white;
}
th
{
border:1px soild white;
border-collapse:collapse;
width:800px;
height:100px;
text-align:center;
background-color:burlywood;
color: white;
}
button {
  background-color: rgb(109, 24, 38); /* Green */
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
}
.add{
  margin-top: 50px;
}
#to19{
  margin-right: 20px;
}

