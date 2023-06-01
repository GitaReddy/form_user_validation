<script>

import 'bootstrap/dist/css/bootstrap.min.css';
	let name = '';
	let email = '';
	let password = '';
	let confirmPassword = '';
	let errors = {};
	let formSubmitted = false;
  
	function validateForm() {
	  errors = {};
  
	  if (!name) {
		errors.name = 'Name is required';
	  }
  
	  if (!email) {
		errors.email = 'Email is required';
	  } else if (!isValidEmail(email)) {
		errors.email = 'Please enter a valid email address';
	  }
  
	  if (!password) {
		errors.password = 'Password is required';
	  } else if (password.length < 8) {
		errors.password = 'Password must be at least 8 characters long';
	  }
  
	  if (password !== confirmPassword) {
		errors.confirmPassword = 'Passwords do not match';
	  }
  
	  // Additional validations...
  
	  return Object.keys(errors).length === 0;
	}
  
	function isValidEmail(email) {
	  // Implement your email validation logic here
	  // Return true if the email is valid, false otherwise

	  const emailRegex = /^[\w-.]+@([\w-]+\.)+[\w-]{2,4}$/;
	 return emailRegex.test(email);

	}
  
	function handleSubmit(event) {
		event.preventDefault();
	  if (validateForm()) {
		// Form is valid, proceed with form submission
		// ...

		displaySubmittedData();
	console.log('Form submitted successfully!');
	formSubmitted = true;
	  }
	}

	function displaySubmittedData() {
		
	 // Get the container element for displaying the submitted data
	 const submittedDataContainer = document.getElementById('submittedData');
	 
	 // Create an HTML string with the submitted data
	 const submittedDataHTML = `
	<h3 Style="padding-top:30px;">Display Information</h3>
	<li><strong>First Name:</strong> ${name}</li>
	<li><strong>Email:</strong> ${email}</li>
	<li><strong>Password:</strong> ${password}</li>
	<li><strong>Confirm Password:</strong> ${confirmPassword}</li>`;
	 
	 // Set the HTML of the container to display the submitted data
	submittedDataContainer.innerHTML = submittedDataHTML;
	}
  </script>
  <div class ="container" >
  <main>
	<form on:submit|preventDefault={handleSubmit}>
		<h1 style="color:#02429E;padding-left:100px">Form Validations</h1>
	  <div>
		<label for="name" class="form-label" >Name</label>
		<input type="text" id="name" bind:value={name} class="form-control"  style ="width:500px"/>
		<div>{#if errors.name}<p class="error" style="color:red;">{errors.name}</p>{/if}</div>
	  </div>
  
	  <div>
		<label for="email" class="form-label">Email</label>
		<input type="email" id="email" bind:value={email} class="form-control" style ="width:500px" />
	<div>{#if errors.email}<p class="error" style="color:red;">{errors.email}</p>{/if}</div>
	  </div>
  
	  <div>
		<label for="password" class="form-label" >Password</label>
		<input type="password" id="password" bind:value={password} class="form-control" style ="width:500px" />
	<div>{#if errors.password}<p class="error" style="color:red;">{errors.password}</p>{/if}</div>
	  </div>
  
	  <div>
		<label for="confirmPassword" class="form-label" >Confirm Password</label>
		<input type="password" id="confirmPassword" bind:value={confirmPassword} class="form-control" style ="width:500px" />
	<div>{#if errors.confirmPassword}<p class="error" style="color:red;">{errors.confirmPassword}</p>{/if}</div>
	  </div>
  <br/>
	  <button type="submit" class="btn btn-primary">Submit</button>
	  <!-- <div id="submittedData" class="submittedData"></div> -->
	</form>
	
  </main>
  <div id="submittedData" class="submittedData"></div>
  </div>
  <style>
	
	/* input{
		padding-top:"10px";
		padding-bottom: "20px";
	} */
  /* label{
	padding-top:"10px";

  } */

	.container{
		padding-left:500px;
	}
  </style>