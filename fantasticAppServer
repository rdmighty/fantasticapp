var express = require('express'); //express framework
var fs = require('fs') ; //file system
var app = express() ; 
var bodyParser = require('body-parser');

app.use(bodyParser.json()); //parsing JSON data

/******************************************************
 * 		    All Web Apis Related to Users			  *
 ******************************************************/	
 
//registering new user
 app.put('/api/RegisterNewUser',function(request,response)
	{
		var recUser = request.body;
		fs.readFile(__dirname+'/resources/json/user.json',function(err,data)
			{
				data = JSON.parse(data.toString());
				console.log(data);
				var found = false;
				var newId = data[data.length-1].id + 1;	 //new id for the user
				var found = false;
				if(recUser.checkEmail) //check for unique email
					{
						for(var i = 1 ; i < data.length ; i ++)
							{
								if(data[i].email == recUser.email) //checking equality with other users
									{
										found = true;
										break;
									}
							}
					}
				if(found)
					{
						response.writeHead(201, {'Content-Type': 'application/json'}); //duplicate name found
						response.end(JSON.stringify({message:"DuplicateEmail"}));
					}
				else
					{
						console.log("New User ID: "+newId);
						recUser.id = newId; //new user id assigned
						data.push(recUser); //pussing new record in previous group
						fs.writeFile(__dirname+'/resources/json/user.json',JSON.stringify(data),function(err) //writing this to file
							{
								if(err)
									{
										response.writeHead(201, {'Content-Type': 'application/json'}); //error writing to the file
										response.end(JSON.stringify({message:"NotCreated"}));
									} //end if
								else
									{
										response.writeHead(200, {'Content-Type': 'application/json'}); //group successfully created
										response.end(JSON.stringify({message:"Created"}));
									}//end else
							})//end writin to file
					}//end else
			})//end reading from file
	}) //end registering user
	
//delete user
app.delete('/api/DeleteThisUser/:id',function(request,response)
	{
		var id = request.params.id;
		console.log("ID: "+id);
		var errorFound = false;
		fs.readFile(__dirname+'/resources/json/group.json',function(err,groupData)
			{
				groupData = JSON.parse(groupData.toString());
				fs.readFile(__dirname+'/resources/json/user.json',function(err,userData)
					{
						userData = JSON.parse(userData.toString());
						
						for(var i = 0 ; i < userData.length ; i ++)
								if(userData[i].id == id)
									{
										userData.splice(i,1);
										break;
									}
									
						for(var i = 0 ; i < groupData.length ; i ++)
							if(groupData[i].group_admin_id == id)
									groupData[i].group_admin_id = "";

						fs.writeFile(__dirname+'/resources/json/group.json',JSON.stringify(groupData),function(err) //writing this to file
							{
								if(err)
									{
										response.writeHead(201, {'Content-Type': 'application/json'}); //error writing to the file
										response.end(JSON.stringify({message:"NotCreated"}));
										errorFound = true;
									}
							})//end writing groupData
							
						if(!errorFound)
							{
								fs.writeFile(__dirname+'/resources/json/user.json',JSON.stringify(userData),function(err) //writing this to file
									{
										if(err)
											{
												response.writeHead(201, {'Content-Type': 'application/json'}); //error writing to the file
												response.end(JSON.stringify({message:"NotCreated"}));
												errorFound = true;
											}
									})//end writing userData
								if(!errorFound)
									{
										response.writeHead(200, {'Content-Type': 'application/json'}); //group successfully created
										response.end(JSON.stringify({message:"Created"}));
									} //end send OK data
							}//end if
						
					})//end reading user
			}) //end reading group
	}) //end deleting

	//update existing user
 app.post('/api/UpdateUser',function(request,response)
	{
		var recUser = request.body;
		fs.readFile(__dirname+'/resources/json/user.json',function(err,data)
			{
				data = JSON.parse(data.toString());
				var found = false;
				var found = false;
				if(recUser.checkEmail) //check for unique name
					{
						for(var i = 0 ; i < data.length ; i ++)
							{
								if(data[i].email == recUser.email) //checking equality with other groups
									{
										found = true;
										break;
									}
							}
					}//end if
				if(found)
					{
						response.writeHead(201, {'Content-Type': 'application/json'}); //duplicate name found
						response.end(JSON.stringify({message:"DuplicateEmail"}));
					}//end if
				if(!found)
					{
						var index = 0 ;
						for(var i = 0 ; i < data.length ; i ++)
							if(data[i].id == recUser.id)
								{
									index = i ;
									break;
								}
						data[index] = (recUser); //updating new record
						fs.writeFile(__dirname+'/resources/json/user.json',JSON.stringify(data),function(err) //writing this to file
							{
								if(err)
									{
										response.writeHead(201, {'Content-Type': 'application/json'}); //error writing to the file
										response.end(JSON.stringify({message:"NotCreated"}));
									}
								else
									{
										response.writeHead(200, {'Content-Type': 'application/json'}); //group successfully created
										response.end(JSON.stringify({newUserData:data[index]}));
									}
							})//end writing to file
					}//end last if
			})//end reading file
	}) //end updating user
	
	//update existing user
 app.post('/api/UpdateUserWithId',function(request,response)
	{
		var recUser = request.body;
		fs.readFile(__dirname+'/resources/json/user.json',function(err,data)
			{
				data = JSON.parse(data.toString());
				var found = false;
				var found = false;
				if(recUser.checkEmail) //check for unique name
					{
						for(var i = 0 ; i < data.length ; i ++)
							{
								if(data[i].email == recUser.email) //checking equality with other groups
									{
										found = true;
										break;
									}
							}
					}//end if
				if(found)
					{
						response.writeHead(201, {'Content-Type': 'application/json'}); //duplicate name found
						response.end(JSON.stringify({message:"DuplicateEmail"}));
					}//end if
				if(!found)
					{
						var index = 0 ;
						for(var i = 0 ; i < data.length ; i ++)
							if(data[i].id == recUser.id)
								{
									index = i ;
									break;
								}
						data[index] = (recUser); //updating new record
						fs.writeFile(__dirname+'/resources/json/user.json',JSON.stringify(data),function(err) //writing this to file
							{
								if(err)
									{
										response.writeHead(201, {'Content-Type': 'application/json'}); //error writing to the file
										response.end(JSON.stringify({message:"NotCreated"}));
									}
								else
									{
										response.writeHead(200, {'Content-Type': 'application/json'}); //group successfully created
										response.end(JSON.stringify({newUserData:data[index]}));
									}
							})//end writing to file
					}//end last if
			})//end reading file
	}) //end updating user
	
//validate login credentials
app.post('/api/PostValidatedUserDetail',function(request, response)
	{
		var username = request.body.userName;
		var password = request.body.password;
		fs.readFile( __dirname+'/resources/json/user.json', function(err, data)
			{
				var data = JSON.parse(data.toString());
				var user = null;
				for(var i = 0 ; i < data.length ; i ++) //searching for user with given credentials
				 {
				  if(data[i].email == username && data[i].password == password)
					{
						user = data[i] ;
						console.log("Found 1 user");
						break;
					}
				 }
				if(user == null)
					{
						console.log("No user found");
						response.writeHead(201, {'Content-Type': 'application/json'}); //no such user found [statusCode:201]
						response.end(JSON.stringify({message:"NotAuthorized"}));
					}
				else
					{
						response.writeHead(200, {'Content-Type': 'application/json'}); //use found with matching credentials [statusCode:200]
						response.end(JSON.stringify(user));
					}
			})
	}) //end validate login credentials

//get all users
app.get('/api/GetUsers',function(request, response)
	{
		fs.readFile( __dirname+'/resources/json/user.json', function(err, data)
			{
				response.writeHead(200, {'Content-Type': 'application/json'}); //all users
				response.end(data.toString());
			})
	})//end get all users
	
//get all users
app.get('/api/GetUser/:id',function(request, response)
	{
		var id = request.params.id;
		fs.readFile( __dirname+'/resources/json/user.json', function(err, data)
			{
				response.writeHead(200, {'Content-Type': 'application/json'}); //all users
				data = JSON.parse(data.toString());
				var index = 0;
				for(var i = 0 ;i  < data.length ; i ++)
					if(data[i].id == id)
						{
							index = i ;
							break;
						}
				response.end(JSON.stringify(data[index]));
			})
	})//end get all users
	
/******************************************************
 * 		    All Web Apis Related to Groups  		  *
 ******************************************************/
 
 //get all groups
 app.get('/api/GetGroups',function(request, response)
	{
		fs.readFile( __dirname+'/resources/json/group.json', function(err, data)
			{
				response.writeHead(200, {'Content-Type': 'application/json'}); //all groups
				response.end(data.toString());
			})
	})//end get all groups
	
 //registering new group
 app.put('/api/RegisterGroup',function(request,response)
	{
		var recGroup = request.body;
		fs.readFile(__dirname+'/resources/json/group.json',function(err,data)
			{
				data = JSON.parse(data.toString());
				console.log(data);
				var newId = 1;
				var found = false;
				if(data.length > 1)
					{
						newId = data[data.length-1].group_id + 1;	
						var found = false;
						if(recGroup.checkName) //check for unique name
							{
								for(var i = 1 ; i < data.length ; i ++)
									{
										if(data[i].group_name == recGroup.group_name) //checking equality with other groups
											{
												found = true;
												break;
											}
									}
							}
						if(found)
							{
								response.writeHead(201, {'Content-Type': 'application/json'}); //duplicate name found
								response.end(JSON.stringify({message:"DuplicateName"}));
							}
						else	
							{
								found = false;
								if(recGroup.checkEmail) //check for unique email
									{
										for(var i = 1 ; i < data.length ; i ++)
											{
												if(data[i].group_email == recGroup.group_email) //check equality with other groups
													{
														found = true;
														break;
													} //end if
											} //end for
									}//end if
								if(found)
									{
										response.writeHead(201, {'Content-Type': 'application/json'}); //duplicate email found
										response.end(JSON.stringify({message:"DuplicateEmail"}));
									}//end if
							}//end else
					}//end if
				if(!found)
					{
						console.log("New Group ID: "+newId);
						recGroup.group_id = newId; //new group id assigned
						data.push(recGroup); //pussing new record in previous group
						fs.writeFile(__dirname+'/resources/json/group.json',JSON.stringify(data),function(err) //writing this to file
							{
								if(err)
									{
										response.writeHead(201, {'Content-Type': 'application/json'}); //error writing to the file
										response.end(JSON.stringify({message:"NotCreated"}));
									} //end if
								else
									{
										response.writeHead(200, {'Content-Type': 'application/json'}); //group successfully created
										response.end(JSON.stringify({message:"Created"}));
									}//end else
							})//end writin to file
					}//end if
			})//end reading from file
	}) //end registering group
 
 //update existing group
 app.post('/api/UpdateGroup',function(request,response)
	{
		var recGroup = request.body;
		fs.readFile(__dirname+'/resources/json/group.json',function(err,data)
			{
				data = JSON.parse(data.toString());
				var found = false;
				if(data.length > 1)
					{
						var found = false;
						if(recGroup.checkName) //check for unique name
							{
								for(var i = 1 ; i < data.length ; i ++)
									{
										if(data[i].group_name == recGroup.group_name) //checking equality with other groups
											{
												found = true;
												break;
											}
									}
							}//end if
						if(found)
							{
								response.writeHead(201, {'Content-Type': 'application/json'}); //duplicate name found
								response.end(JSON.stringify({message:"DuplicateName"}));
							}//end if
						else	
							{
								found = false;
								if(recGroup.checkEmail) //check for unique email
									{
										for(var i = 1 ; i < data.length ; i ++)
											{
												if(data[i].group_email == recGroup.group_email) //check equality with other groups
													{
														found = true;
														break;
													}
											}
									}
								if(found)
									{
										response.writeHead(201, {'Content-Type': 'application/json'}); //duplicate email found
										response.end(JSON.stringify({message:"DuplicateEmail"}));
									}
							}//end else
					}//end if
				if(!found)
					{
						var index = 0 ;
						for(var i = 0 ; i < data.length ; i ++)
							if(data[i].group_id == recGroup.group_id)
								{
									index = i ;
									break;
								}
						data[index] = (recGroup); //updating new record
						fs.writeFile(__dirname+'/resources/json/group.json',JSON.stringify(data),function(err) //writing this to file
							{
								if(err)
									{
										response.writeHead(201, {'Content-Type': 'application/json'}); //error writing to the file
										response.end(JSON.stringify({message:"NotCreated"}));
									}
								else
									{
										response.writeHead(200, {'Content-Type': 'application/json'}); //group successfully created
										response.end(JSON.stringify({message:"Created"}));
									}
							})//end writing to file
					}//end last if
			})//end reading file
	}) //end updating group
 
 //delete existing group
 app.delete('/api/DeleteGroup/:id',function(request,response)
	{
		var id = request.params.id;
		console.log("ID: "+id);
		var errorFound = false;
		fs.readFile(__dirname+'/resources/json/group.json',function(err,groupData)
			{
				groupData = JSON.parse(groupData.toString());
				fs.readFile(__dirname+'/resources/json/user.json',function(err,userData)
					{
						userData = JSON.parse(userData.toString());
						for(var i = 0 ; i < userData.length ; i ++)
							if(userData[i].group_id == id)
								userData[i].group_id = "";
						for(var i = 0 ; i < groupData.length ; i ++)
							if(groupData[i].group_id == id)
								{
									groupData.splice(i,1);
									break;
								}
						fs.writeFile(__dirname+'/resources/json/group.json',JSON.stringify(groupData),function(err) //writing this to file
							{
								if(err)
									{
										response.writeHead(201, {'Content-Type': 'application/json'}); //error writing to the file
										response.end(JSON.stringify({message:"NotCreated"}));
										errorFound = true;
									}
							})//end writing groupData
						if(!errorFound)
							{
								fs.writeFile(__dirname+'/resources/json/user.json',JSON.stringify(userData),function(err) //writing this to file
									{
										if(err)
											{
												response.writeHead(201, {'Content-Type': 'application/json'}); //error writing to the file
												response.end(JSON.stringify({message:"NotCreated"}));
												errorFound = true;
											}
									})//end writing userData
								if(!errorFound)
									{
										response.writeHead(200, {'Content-Type': 'application/json'}); //group successfully created
										response.end(JSON.stringify({message:"Created"}));
									} //end send OK data
							}//end if
						
					})//end reading user
			}) //end reading group
	}) //end deleting
//creating server
var server = app.listen(9485, function()
	{
		var port = server.address().port;
		console.log('Server listening at port: '+port);
	})
