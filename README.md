import React, { useState } from 'react';

const FormComponent = () => {
  // State variables to store form data
  const [formData, setFormData] = useState({
    name: '',
    email: '',
    password: '',
    confirmPassword: ''
  });

  // State variable to store form validation errors
  const [errors, setErrors] = useState({});

  // Function to handle form input changes
  const handleInputChange = (e) => {
    const { name, value } = e.target;
    setFormData({
      ...formData,
      [name]: value
    });
  };

  // Function to handle form submission
  const handleSubmit = (e) => {
    e.preventDefault();

    // Form validation
    const validationErrors = {};
    if (!formData.name.trim()) {
      validationErrors.name = 'Name is required';
    }
    if (!formData.email.trim()) {
      validationErrors.email = 'Email is required';
    } else if (!/\S+@\S+\.\S+/.test(formData.email)) {
      validationErrors.email = 'Email is invalid';
    }
    if (!formData.password.trim()) {
      validationErrors.password = 'Password is required';
    } else if (formData.password.trim().length < 8) {
      validationErrors.password = 'Password must be at least 8 characters long';
    }
    if (!formData.confirmPassword.trim()) {
      validationErrors.confirmPassword = 'Please confirm your password';
    } else if (formData.confirmPassword !== formData.password) {
      validationErrors.confirmPassword = 'Passwords do not match';
    }

    if (Object.keys(validationErrors).length > 0) {
      // If there are validation errors, set errors state and return
      setErrors(validationErrors);
      return;
    }

    // If no validation errors, display form data in alert
    alert(JSON.stringify(formData));

    // Clear form data
    setFormData({
      name: '',
      email: '',
      password: '',
      confirmPassword: ''
    });

    // Clear errors
    setErrors({});
  };

  return (
    <form onSubmit={handleSubmit}>
      <div>
        <label htmlFor="name">Name:</label>
        <input 
          type="text" 
          id="name" 
          name="name" 
          value={formData.name} 
          onChange={handleInputChange} 
        />
        {errors.name && <div>{errors.name}</div>}
      </div>
      <div>
        <label htmlFor="email">Email:</label>
        <input 
          type="email" 
          id="email" 
          name="email" 
          value={formData.email} 
          onChange={handleInputChange} 
        />
        {errors.email && <div>{errors.email}</div>}
      </div>
      <div>
        <label htmlFor="password">Password:</label>
        <input 
          type="password" 
          id="password" 
          name="password" 
          value={formData.password} 
          onChange={handleInputChange} 
        />
        {errors.password && <div>{errors.password}</div>}
      </div>
      <div>
        <label htmlFor="confirmPassword">Confirm Password:</label>
        <input 
          type="password" 
          id="confirmPassword" 
          name="confirmPassword" 
          value={formData.confirmPassword} 
          onChange={handleInputChange} 
        />
        {errors.confirmPassword && <div>{errors.confirmPassword}</div>}
      </div>
      <button type="submit">Submit</button>
    </form>
  );
};

export default FormComponent;
