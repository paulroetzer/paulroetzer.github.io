---
layout: page
icon: fas fa-info-circle
order: 1
---

![Desktop View](/assets/img/avatar.jpeg){: width="512" height="512" .w-50 .left}

I am a third year PhD Student supervised by <a href="https://lovc.cs.uni-bonn.de/index.php/team/florian-bernard/">Professor Florian Bernard</a> at the University of Bonn. I work with graphs (and graph algorithms), on correspondence problems, and on optimisation methods, all focused on problems in 3D space.

Previously, I received my Master's degree in Robotics, Cognition, Intelligence as well as my Bachelor's degree in Mechanical Engineering at Technical University of Munich (TUM).

Apart from researching, I love to run, bike, and swim.

<br>
# News
{% assign pinned = site.posts | where: 'pin', 'true' %}
{% assign default = site.posts | where_exp: 'item', 'item.pin != true and item.hidden != true' %}

{% assign news = '' | split: '' %}
{% assign posts = '' | split: '' %}

<!-- pinned posts are news -->
{% assign offset = paginator.page | minus: 1 | times: paginator.per_page %}
{% assign pinned_num = pinned.size | minus: offset %}

{% if pinned_num > 0 %}
  {% for i in (offset..pinned.size) limit: pinned_num %}
    {% assign news = news | push: pinned[i] %}
  {% endfor %}
{% else %}
  {% assign pinned_num = 0 %}
{% endif %}

<!-- Get default posts -->
{% assign default_beg = offset | minus: pinned.size %}

{% if default_beg < 0 %}
  {% assign default_beg = 0 %}
{% endif %}

{% assign default_num = paginator.posts | size | minus: pinned_num %}
{% assign default_end = default_beg | plus: default_num | minus: 1 %}

{% if default_num > 0 %}
  {% for i in (default_beg..default_end) %}
    {% assign posts = posts | push: default[i] %}
  {% endfor %}
{% endif %}

<div id="post-list">
  {% for post in news %}
    <a href="{{ post.url | relative_url }}" class="card-wrapper" style="min-height: 5rem !important; min-height: 6rem !important;">
      <div class="card post-preview flex-md-row-reverse">
        <div class="card-body d-flex flex-column">
          <h1 class="card-title my-2 mt-md-0">
            {{ post.title }}
          </h1>

          <div class="card-text post-content mt-0 mb-2">
            <p>
              {% include no-linenos.html content=post.content %}
              {{ content | markdownify | strip_html | truncate: 200 | escape }}
            </p>
          </div>

          <div class="post-meta flex-grow-1 d-flex align-items-end">
            <div class="me-auto">
              <!-- posted date -->
              <i class="far fa-calendar fa-fw me-1"></i>
              {% include datetime.html date=post.date lang=lang %}
            </div>
          </div>
          <!-- .post-meta -->
        </div>
        <!-- .card-body -->
      </div>
    </a>
  {% endfor %}
</div>
<!-- #post-list -->
<!-- #post-list -->

<div id="post-list">
  {% for post in posts %}
    <a href="{{ post.url | relative_url }}" class="card-wrapper">
      <div class="card post-preview flex-md-row-reverse">
        {% if post.image %}
          {% if post.image.lqip %}
            {% capture lqip %}lqip="{{ post.image.lqip }}"{% endcapture %}
          {% endif %}

          {% assign src = post.image.path | default: post.image %}
          {% unless src contains '//' %}
            {% assign src = post.img_path | append: '/' | append: src | replace: '//', '/' %}
          {% endunless %}

          {% assign alt = post.image.alt | xml_escape | default: 'Preview Image' %}

          <img src="{{ src }}" w="17" h="10" alt="{{ alt }}" {{ lqip }}>
        {% endif %}

        <div class="card-body d-flex flex-column">
          <h1 class="card-title my-2 mt-md-0">
            {{ post.title }}
          </h1>

          <div class="card-text post-content mt-0 mb-2">
            <p>
              {% include no-linenos.html content=post.content %}
              {{ content | markdownify | strip_html | truncate: 200 | escape }}
            </p>
          </div>

          <div class="post-meta flex-grow-1 d-flex align-items-end">
            <div class="me-auto">
              <!-- posted date -->
              <i class="far fa-calendar fa-fw me-1"></i>
              {% include datetime.html date=post.date lang=lang %}

              <!-- categories -->
              {% if post.categories.size > 0 %}
                <i class="far fa-folder-open fa-fw me-1"></i>
                <span class="categories">
                  {% for category in post.categories %}
                    {{ category }}
                    {%- unless forloop.last -%},{%- endunless -%}
                  {% endfor %}
                </span>
              {% endif %}
            </div>

            {% if post.pin %}
              <div class="pin ms-1">
                <i class="fas fa-thumbtack fa-fw"></i>
                <span>{{ site.data.locales[lang].post.pin_prompt }}</span>
              </div>
            {% endif %}
          </div>
          <!-- .post-meta -->
        </div>
        <!-- .card-body -->
      </div>
    </a>
  {% endfor %}
</div>
<!-- #post-list -->
