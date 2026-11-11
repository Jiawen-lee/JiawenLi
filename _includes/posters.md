<h2 id="posters">Posters</h2>
<div class="publications">
  <ol class="bibliography">
    {% for link in site.data.posters.main %}
    <li>
      <article class="pub-row{% unless link.image %} pub-row-text-only{% endunless %}">
        {% if link.image %}
        <a class="publication-figure" href="{{ link.image }}" aria-label="View full figure for {{ link.title | escape }}">
          <img src="{{ link.image }}" class="teaser" alt="Research overview for {{ link.title | escape }}" loading="lazy" decoding="async">
        </a>
        {% endif %}
        <div class="publication-details">
          <h3 class="title">{% if link.pdf %}<a href="{{ link.pdf }}">{{ link.title }}</a>{% else %}{{ link.title }}{% endif %}</h3>
          <div class="author">{{ link.authors }}</div>
          <div class="periodical">{{ link.conference }}</div>
          <div class="links">
            {% if link.pdf %}<a href="{{ link.pdf }}" class="btn" target="_blank" rel="noopener">PDF</a>{% endif %}
            {% if link.code %}<a href="{{ link.code }}" class="btn" target="_blank" rel="noopener">Code</a>{% endif %}
            {% if link.page %}<a href="{{ link.page }}" class="btn" target="_blank" rel="noopener">Project Page</a>{% endif %}
            {% if link.bibtex %}<a href="{{ link.bibtex }}" class="btn" target="_blank" rel="noopener">BibTeX</a>{% endif %}
            {% if link.notes %}<strong class="publication-note">{{ link.notes }}</strong>{% endif %}
            {% if link.others %}{{ link.others }}{% endif %}
          </div>
        </div>
      </article>
    </li>
    {% endfor %}
  </ol>
</div>
