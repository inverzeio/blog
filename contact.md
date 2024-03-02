---
layout: page
title: contact
permalink: /contact/
---

------------

<form class="contact-form" method="POST" data-netlify="true" data-netlify-recaptcha="true">
  <div>
    <input id="name" name="name" type="text" required>
    <label for="name">Your Name *</label>
  </div>
    <div>
    <input id="email" name="email" type="mail" required>
    <label for="email">E-mail Address *</label>
  </div>
  <div>
    <input id="phone" name="phone" type="tel" required>
    <label for="phone">Primary Phone</label>
  </div>
  <div>
    <textarea rows="4" cols="100" id="message" name="message" type="text" required></textarea>
    <label for="message">Message *</label>
  </div>
    <div data-netlify-recaptcha="true"></div>
  <p>
    <button type="submit">Send</button>
  </p>
</form>
