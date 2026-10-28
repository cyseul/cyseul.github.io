<h2 id="news">News</h2>
{% comment %} Show entries from the last 6 months (based on build time); always show at least 3. Older entries are collapsed. {% endcomment %}
{% assign news_min_visible = 3 %}
{% assign news_cutoff = site.time | date: "%s" | minus: 15778800 %}
{% assign news_sorted = site.data.news %}
<ul class="news-list">
{% for item in news_sorted %}
{% assign item_ts = item.date | date: "%s" | plus: 0 %}
{% if item_ts >= news_cutoff or forloop.index <= news_min_visible %}
<li><strong>[{{ item.label }}]</strong> {{ item.text }}</li>
{% endif %}
{% endfor %}
</ul>
{% assign news_hidden = 0 %}
{% for item in news_sorted %}
{% assign item_ts = item.date | date: "%s" | plus: 0 %}
{% if item_ts < news_cutoff and forloop.index > news_min_visible %}
{% assign news_hidden = news_hidden | plus: 1 %}
{% endif %}
{% endfor %}
{% if news_hidden > 0 %}
<ul class="news-list" id="news-more" style="display: none;">
{% for item in news_sorted %}
{% assign item_ts = item.date | date: "%s" | plus: 0 %}
{% if item_ts < news_cutoff and forloop.index > news_min_visible %}
<li><strong>[{{ item.label }}]</strong> {{ item.text }}</li>
{% endif %}
{% endfor %}
</ul>
<p style="margin-top: 0;"><a href="#news" id="news-toggle" style="font-size: 0.9em;" onclick="var m=document.getElementById('news-more');var h=m.style.display==='none';m.style.display=h?'':'none';this.textContent=h?'Show less':'Show more';return false;">Show more</a></p>
{% endif %}
