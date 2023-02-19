---
title: pages.contact
layout: page

namespace: contact

permalink: "/contato"
permalink_en: "/contact"
comments: false
---

<form action="https://formspree.io/f/{{site.formspree_id}}" method="POST">
<p class="mb-4">{% t contact.start_text %} {% t site.name %}. {% t contact.finish_text %}</p>
<div class="form-group row">
<div class="col-md-6">
<input class="form-control" type="text" name="name" placeholder="Nome*" required>
</div>
<div class="col-md-6">
<input class="form-control" type="email" name="_replyto" placeholder="E-mail*" required>
</div>
</div>
<textarea rows="8" class="form-control mb-3" name="message" placeholder="Menssagem*" required></textarea>
<!-- <div class="g-recaptcha" data-sitekey="{{site.recaptcha_key}}"></div> -->
<br />
<input class="btn btn-dark" type="submit" value="Send">
</form>
