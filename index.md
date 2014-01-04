---
layout: page
title: Tim Banks
tagline: Supporting tagline
---

<div id="hello">
    <div class="container">
        <div class="row">
            <div class="col-lg-8 col-lg-offset-2 centered">
                <h1>The hard part is what separates good from great.</h1>
                <h2>Noah Kagan</h2>
            </div>
        </div>
    </div>
</div>

<div id="green">
    <div class="container">
        <div class="row">        
            <div class="col-lg-12 centered">
                <h3>WHO AM I?</h3>
                <p>Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book.</p>
            </div>
        </div>
    </div>
</div>
  
<div class="container">
    <div class="row centered mt grid">
        <h3>Latest Posts</h3>
        
        <div class="posts">
          {% for post in site.posts limit:5%}
            <div class="post">
                <h3><a href="{{ BASE_PATH }}{{ post.url }}">{{ post.title }}</a></h3>
                <p>{{ post.date | date_to_string }}</p>
            </div>
          {% endfor %}
        </div>
    </div>
</div>