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
		<label for="name" class="label" style= "padding-bottom:10px !important">Name</label>
		<input type="text" id="name" placeholder="Name" bind:value={name} class="form-control"  style ="width:500px"/>
		{#if errors.name}<div class="error" style="color:red;padding-bottom:8px !important">{errors.name}</div>{/if}
	  </div>
  
	  <div>
		<label for="email" class="label" style= "padding-bottom:10px !important">Email</label>
		<input type="email" id="email" placeholder="Email" bind:value={email} class="form-control" style ="width:500px" />
	{#if errors.email}<div class="error" style="color:red;padding-bottom:8px !important">{errors.email}</div>{/if}
	  </div>
  
	  <div>
		<label for="password" class="label" style= "padding-bottom:10px !important">Password</label>
		<input type="password" id="password" placeholder="Password" bind:value={password} class="form-control" style ="width:500px" />
	{#if errors.password}<div class="error" style="color:red;padding-bottom:8px !important">{errors.password}</div>{/if}
	  </div>
  
	  <div>
		<label for="confirmPassword" class="label" style= "padding-bottom:10px !important">Confirm Password</label>
		<input type="password" id="confirmPassword"  placeholder="Confirm Password" bind:value={confirmPassword} class="form-control" style ="width:500px" />
	{#if errors.confirmPassword}<div class="error" style="color:red;padding-bottom:8px !important">{errors.confirmPassword}</div>{/if}
	  </div>
  <br/>
	  <button type="submit" class="btn btn-primary">Submit</button>
	  
	</form>
	
  </main>
  <div id="submittedData" class="submittedData"></div>
  </div>
  <style>
	
	/* input{
		padding-top:"10px";
		padding-bottom: "20px";
	} */
  

	.container{
		padding-left:500px;
	}
  </style>