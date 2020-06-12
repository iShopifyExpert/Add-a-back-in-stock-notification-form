#Sectioned themes

Viewing or changing where notifications are sent

When a customer submits the back in stock notification form for a sold out product, you will receive an email to the email address you have specified in the admin in the Customer email field.

stock-sec01.jpg

To view or change your Customer email, from your Shopify admin, click Settings, then click General.
 

Adding the notification form code to your theme
 

 

From your Shopify admin, go to Online Store > Themes.
Find the theme you want to edit, and then click Actions > Edit code.
In the Sections directory, click product-template.liquid.
Find the opening HTML <form> tag. It will look similar to this:

{% form 'product', product, class:form_classes, novalidate: 'novalidate', data-product-form: '' %}
 

Wrap the opening <form> tag in conditional Liquid tags, so that on a new line above it is {% if product.available %}, and on a new line below it is {% endif %}. Your code should look like this:

{% if product.available %}
{% form 'product', product, class:form_classes, novalidate: 'novalidate', data-product-form: '' %}
{% endif %}
 

Find the closing HTML </form> tag. Wrap it in conditional Liquid tags, so that on a new line above it is {% if product.available %}, and on a new line below it is {% endif %}. Your code should look like this:

{% if product.available %}
{% endform %}
{% endif %}
 

Find the product title in the code by looking for {{ product.title }}. On a new line below the line of code that contains the product title, paste the following code:

{% unless product.available %}
<div id="sold-out">
  {% form 'contact' %}
    {% if form.posted_successfully? %}
    <p class="accent-text">Thanks! We will notify you when this product becomes available!</p>
    {% else %}
    <p>Click <a id="notify-me" href="#"><strong>here</strong></a> to be notified by email when {{ product.title }} becomes available.</p>
    {% endif %}
    {% if form.errors %}
    <div class="error feedback accent-text">
      <p>Please provide a valid email address.</p>
    </div>
    {% endif %}
    {% unless form.posted_successfully? %}
    <div id="notify-me-wrapper" class="clearfix" style="display:none">
      {% if customer %}
      <input type="hidden" name="contact[email]" value="{{ customer.email }}" />
      {% else %}
      <input style="float:left; width:180px;" required="required" type="email" name="contact[email]" placeholder="your@email.com" class="styled-input{% if form.errors contains 'email' %} error{% endif %}" value="{{ contact.fields.email }}" />
      {% endif %}
      <input type="hidden" name="contact[body]" value="Please notify me when {{ product.title | escape }} becomes available." />
      <input style="float:left; margin-left:5px;" class="btn styled-submit" type="submit" value="Send" />
    </div>
    {% endunless %}
  {% endform %}
</div>
{% endunless %}
 

You can experiment with placing the code in different areas of the file to have the notification form display in a different position on the product page.
Click Save.
In the Assets directory, click theme.js, or theme.js.liquid.
At the very bottom of the file, paste the following code:

jQuery('#notify-me').click(function() {

jQuery('#notify-me-wrapper').fadeIn();

return false;
} );
 

Click Save.


=================================================


#Non-sectioned themes 

Viewing or changing where notifications are sent

When a customer submits the back in stock notification form for a sold out product, you will receive an email to the email address you have specified in the admin in the Customer email field.

stock-sec01.jpg

To view or change your Customer email, from your Shopify admin, click Settings, then click General.

Adding the notification form code to your theme
 

 

From your Shopify admin, go to Online Store > Themes.
Find the theme you want to edit, and then click Actions > Edit code.
In the Sections directory, click product-template.liquid.
Find the opening HTML <form> tag. It will look similar to this:

{% form 'product', product, class:form_classes, novalidate: 'novalidate', data-product-form: '' %}
 

Wrap the opening <form> tag in conditional Liquid tags, so that on a new line above it is {% if product.available %}, and on a new line below it is {% endif %}. Your code should look like this:

{% if product.available %}
{% form 'product', product, class:form_classes, novalidate: 'novalidate', data-product-form: '' %}
{% endif %}
 

Find the closing HTML </form> tag. Wrap it in conditional Liquid tags, so that on a new line above it is {% if product.available %}, and on a new line below it is {% endif %}. Your code should look like this:

{% if product.available %}
{% endform %}
{% endif %}
 

Find the product title in the code by looking for {{ product.title }}. On a new line below the line of code that contains the product title, paste the following code:

{% unless product.available %}
<div id="sold-out">
  {% form 'contact' %}
    {% if form.posted_successfully? %}
    <p class="accent-text">Thanks! We will notify you when this product becomes available!</p>
    {% else %}
    <p>Click <a id="notify-me" href="#"><strong>here</strong></a> to be notified by email when {{ product.title }} becomes available.</p>
    {% endif %}
    {% if form.errors %}
    <div class="error feedback accent-text">
      <p>Please provide a valid email address.</p>
    </div>
    {% endif %}
    {% unless form.posted_successfully? %}
    <div id="notify-me-wrapper" class="clearfix" style="display:none">
      {% if customer %}
      <input type="hidden" name="contact[email]" value="{{ customer.email }}" />
      {% else %}
      <input style="float:left; width:180px;" required="required" type="email" name="contact[email]" placeholder="your@email.com" class="styled-input{% if form.errors contains 'email' %} error{% endif %}" value="{{ contact.fields.email }}" />
      {% endif %}
      <input type="hidden" name="contact[body]" value="Please notify me when {{ product.title | escape }} becomes available." />
      <input style="float:left; margin-left:5px;" class="btn styled-submit" type="submit" value="Send" />
    </div>
    {% endunless %}
  {% endform %}
</div>
{% endunless %}
 

You can experiment with placing the code in different areas of the file to have the notification form display in a different position on the product page.
Click Save.
In the Assets directory, click theme.js, or theme.js.liquid.
At the very bottom of the file, paste the following code:

jQuery('#notify-me').click(function() {

jQuery('#notify-me-wrapper').fadeIn();

return false;
} );
 

Click Save.
