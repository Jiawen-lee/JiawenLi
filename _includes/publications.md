<h2 id="publications" style="margin: 2px 0px 10px;">Publications and Preprints</h2>

<div class="publications" style="max-width: 1000px; margin: 0 auto;">  <!-- Wider layout -->
  <ol class="bibliography">
    {% for link in site.data.publications.main %}
    <li style="list-style: none; margin-bottom: 40px;">
      <div class="pub-row" style="display: flex; flex-wrap: wrap; align-items: flex-start;">
        <div style="flex: 0 0 48%; max-width: 40%; padding: 0;">
          {% if link.image %}
          <div style="width: 100%; height: 160px; border: 1px solid #ccc; border-radius: 10px; background: white; overflow: hidden;">
            <img src="{{ link.image }}" 
                 class="teaser"
                 style="width: 100%; height: 100%; object-fit: cover; object-position: center;">
          </div>
          {% endif %}
        </div>
        <div class="col-sm-8" style="flex: 1; padding: 0 20px;">
          <div class="title" style="font-weight: bold; font-size: 16px; margin-bottom: 5px;">
            <a href="{{ link.pdf }}" >{{ link.title }}</a>
          </div>
          <div class="author" style="font-size: 14px; margin-bottom: 5px;">{{ link.authors }}</div>
          <div class="periodical" style="font-size: 13px; color: #aaa; margin-bottom: 10px;">
            <em>{{ link.conference }}</em>
          </div>
          <div class="links">
            {% if link.pdf %} 
            <a href="{{ link.pdf }}" class="btn btn-sm" role="button" target="_blank" style="font-size:12px;">PDF</a>
            {% endif %}
            {% if link.code %} 
            <a href="{{ link.code }}" class="btn btn-sm" role="button" target="_blank" style="font-size:12px;">Code</a>
            {% endif %}
            {% if link.page %} 
            <a href="{{ link.page }}" class="btn btn-sm" role="button" target="_blank" style="font-size:12px;">Project Page</a>
            {% endif %}
            {% if link.bibtex %} 
            <a href="{{ link.bibtex }}" class="btn btn-sm" role="button" target="_blank" style="font-size:12px;">BibTex</a>
            {% endif %}
            {% if link.notes %} 
            <strong><i style="color:#e74d3c">{{ link.notes }}</i></strong>
            {% endif %}
            {% if link.others %} 
            {{ link.others }}
            {% endif %}
          </div>
        </div>
      </div>
    </li>
    {% endfor %}
  </ol>
</div>
