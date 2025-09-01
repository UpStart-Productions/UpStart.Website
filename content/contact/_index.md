---
title: "Contact Us"
description: "Get in touch with UpStart Productions to discuss your next project"
slug: "contact"
draft: false
---

{{< aos-wrapper animation="fade-up" duration="1000" >}}
# Contact Us

Ready to start your next project? We'd love to hear from you. Get in touch and let's discuss how we can help bring your vision to life.
{{< /aos-wrapper >}}

<div class="grid grid-cols-1 lg:grid-cols-2 gap-12 mt-8">

{{< aos-wrapper animation="fade-right" duration="1000" delay="200" >}}
<div>
  <h2 class="text-2xl font-bold mb-6">Get In Touch</h2>
  
  <!-- Contact Form - Placeholder for AWS Lambda integration -->
  <form id="contact-form" class="space-y-6">
    <div>
      <label for="name" class="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-2">Full Name</label>
      <input type="text" id="name" name="name" required 
             class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent dark:bg-gray-800 dark:border-gray-600 dark:text-white">
    </div>
    
    <div>
      <label for="email" class="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-2">Email Address</label>
      <input type="email" id="email" name="email" required 
             class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent dark:bg-gray-800 dark:border-gray-600 dark:text-white">
    </div>
    
    <div>
      <label for="company" class="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-2">Company (Optional)</label>
      <input type="text" id="company" name="company" 
             class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent dark:bg-gray-800 dark:border-gray-600 dark:text-white">
    </div>
    
    <div>
      <label for="service" class="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-2">Service Interest</label>
      <select id="service" name="service" 
              class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent dark:bg-gray-800 dark:border-gray-600 dark:text-white">
        <option value="">Select a service</option>
        <option value="web-development">Web Development</option>
        <option value="product-design">Product Design</option>
        <option value="technology-consulting">Technology Consulting</option>
        <option value="nepho-platform">Nepho Platform</option>
        <option value="other">Other</option>
      </select>
    </div>
    
    <div>
      <label for="message" class="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-2">Message</label>
      <textarea id="message" name="message" rows="5" required 
                class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-transparent dark:bg-gray-800 dark:border-gray-600 dark:text-white"
                placeholder="Tell us about your project..."></textarea>
    </div>
    
    <button type="submit" 
            class="w-full bg-blue-600 text-white py-3 px-6 rounded-lg hover:bg-blue-700 transition-colors font-medium">
      Send Message
    </button>
  </form>
  
  <!-- Success/Error Messages -->
  <div id="form-success" class="hidden mt-4 p-4 bg-green-100 text-green-700 rounded-lg">
    Thank you for your message! We'll get back to you within 24 hours.
  </div>
  
  <div id="form-error" class="hidden mt-4 p-4 bg-red-100 text-red-700 rounded-lg">
    There was an error sending your message. Please try again or contact us directly.
  </div>
</div>
{{< /aos-wrapper >}}

{{< aos-wrapper animation="fade-left" duration="1000" delay="400" >}}
<div>
  <h2 class="text-2xl font-bold mb-6">Other Ways to Reach Us</h2>
  
  <div class="space-y-6">
    <div class="flex items-start space-x-4">
      <div class="w-8 h-8 bg-blue-500 rounded-full flex items-center justify-center flex-shrink-0 mt-1">
        <span class="text-white text-sm">📧</span>
      </div>
      <div>
        <h3 class="font-medium text-gray-900 dark:text-white">Email</h3>
        <p class="text-gray-600 dark:text-gray-400">hello@upstartproductions.com</p>
        <p class="text-sm text-gray-500 dark:text-gray-500">We respond within 24 hours</p>
      </div>
    </div>
    
    <div class="flex items-start space-x-4">
      <div class="w-8 h-8 bg-green-500 rounded-full flex items-center justify-center flex-shrink-0 mt-1">
        <span class="text-white text-sm">📱</span>
      </div>
      <div>
        <h3 class="font-medium text-gray-900 dark:text-white">Phone</h3>
        <p class="text-gray-600 dark:text-gray-400">+1 (555) 123-4567</p>
        <p class="text-sm text-gray-500 dark:text-gray-500">Monday - Friday, 9AM - 6PM EST</p>
      </div>
    </div>
    
    <div class="flex items-start space-x-4">
      <div class="w-8 h-8 bg-purple-500 rounded-full flex items-center justify-center flex-shrink-0 mt-1">
        <span class="text-white text-sm">🏢</span>
      </div>
      <div>
        <h3 class="font-medium text-gray-900 dark:text-white">Office</h3>
        <p class="text-gray-600 dark:text-gray-400">123 Innovation Drive<br>Tech City, TC 12345</p>
        <p class="text-sm text-gray-500 dark:text-gray-500">By appointment only</p>
      </div>
    </div>
  </div>
  
  <div class="mt-8 p-6 bg-gray-50 dark:bg-gray-800 rounded-lg">
    <h3 class="font-medium text-gray-900 dark:text-white mb-3">Quick Response</h3>
    <p class="text-sm text-gray-600 dark:text-gray-400">
      For urgent inquiries or immediate assistance with existing projects, 
      please call us directly. For new project discussions, the contact form 
      or email works best as it allows us to gather initial requirements.
    </p>
  </div>
</div>
{{< /aos-wrapper >}}

</div>

<!-- JavaScript for form handling - TODO: Replace with AWS Lambda endpoint -->
<script>
document.getElementById('contact-form').addEventListener('submit', function(e) {
    e.preventDefault();
    
    // TODO: Replace this with actual AWS Lambda endpoint
    // const lambdaEndpoint = 'https://your-api-gateway-url.amazonaws.com/prod/contact';
    
    // Placeholder success behavior
    document.getElementById('form-success').classList.remove('hidden');
    document.getElementById('form-error').classList.add('hidden');
    this.reset();
    
    // Actual implementation will look like:
    /*
    const formData = new FormData(this);
    const data = Object.fromEntries(formData.entries());
    
    fetch(lambdaEndpoint, {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json',
        },
        body: JSON.stringify(data)
    })
    .then(response => response.json())
    .then(data => {
        if (data.success) {
            document.getElementById('form-success').classList.remove('hidden');
            document.getElementById('form-error').classList.add('hidden');
            this.reset();
        } else {
            throw new Error('Form submission failed');
        }
    })
    .catch(error => {
        document.getElementById('form-error').classList.remove('hidden');
        document.getElementById('form-success').classList.add('hidden');
    });
    */
});
</script>
