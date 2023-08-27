---
# the default layout is 'page'
icon: fas fa-envelope
order: 5
---

<!-- <form action="https://formspree.io/{{site.email}}" method="POST"> -->
<form action="https://formspree.io/f/mgedykzb" method="POST">
<!-- <p class="mb-4">Please send your message to {{ site.title }}. We will reply as soon as possible!</p> -->
<p class="mb-4">Silahkan kirim pesan Anda ke {{ site.title }}. Kami akan berusaha membalas secepatnya! </p>
<div class="form-group row">
<div class="col-md-6">
<input class="form-control" type="text" name="name" placeholder="Nama*" required>
</div>
<div class="col-md-6">
<input class="form-control" type="email" name="_replyto" placeholder="Alamat E-mail*" required>
</div>
</div>
<textarea rows="8" class="form-control mb-3" name="message" placeholder="Pesan*" required></textarea>    
<input class="btn btn-dark" type="submit" value="Send">
</form>