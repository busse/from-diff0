---
layout: default
title: Notes
permalink: /notes/
---

<div class="row">
    <div class="col-lg-10 mx-auto">
        <div class="d-flex justify-content-between align-items-center mb-4">
            <h1>Notes</h1>
            <div class="text-muted">{{ site.notes | size }} notes</div>
        </div>

        <p class="lead">A collection of interconnected notes following the Zettelkasten method. Each note contains atomic ideas that link to related concepts.</p>

        <!-- Search Box -->
        <div class="mb-4">
            <input type="text" class="form-control" id="noteSearch" placeholder="Search notes by title, content, or tags...">
        </div>

        <!-- Filter Options -->
        <div class="mb-4">
            <div class="row">
                <div class="col-md-6">
                    <label for="categoryFilter" class="form-label">Filter by Category:</label>
                    <select class="form-select" id="categoryFilter">
                        <option value="">All Categories</option>
                        {% assign categories = site.notes | map: 'categories' | flatten | uniq | sort %}
                        {% for category in categories %}
                            <option value="{{ category }}">{{ category | capitalize }}</option>
                        {% endfor %}
                    </select>
                </div>
                <div class="col-md-6">
                    <label for="tagFilter" class="form-label">Filter by Tag:</label>
                    <select class="form-select" id="tagFilter">
                        <option value="">All Tags</option>
                        {% assign tags = site.notes | map: 'tags' | flatten | uniq | sort %}
                        {% for tag in tags %}
                            <option value="{{ tag }}">{{ tag }}</option>
                        {% endfor %}
                    </select>
                </div>
            </div>
        </div>

        <!-- Notes Grid -->
        <div class="row" id="notesContainer">
            {% assign sorted_notes = site.notes | sort: 'date' | reverse %}
            {% for note in sorted_notes %}
                <div class="col-md-6 col-lg-4 mb-4 note-card" 
                     data-title="{{ note.title | downcase }}"
                     data-content="{{ note.content | strip_html | downcase | truncate: 200 }}"
                     data-tags="{{ note.tags | join: ' ' | downcase }}"
                     data-categories="{{ note.categories | join: ' ' | downcase }}">
                    <div class="card h-100">
                        <div class="card-body">
                            <h5 class="card-title">
                                <a href="{{ note.url | relative_url }}" class="text-decoration-none">{{ note.title }}</a>
                            </h5>
                            {% if note.date %}
                                <p class="card-text"><small class="text-muted">{{ note.date | date: "%B %d, %Y" }}</small></p>
                            {% endif %}
                            <p class="card-text">{{ note.content | strip_html | truncate: 120 }}</p>
                        </div>
                        <div class="card-footer bg-transparent">
                            {% if note.categories %}
                                {% for category in note.categories %}
                                    <span class="badge bg-primary me-1">{{ category }}</span>
                                {% endfor %}
                            {% endif %}
                            {% if note.tags %}
                                {% for tag in note.tags limit:3 %}
                                    <span class="badge bg-secondary me-1">#{{ tag }}</span>
                                {% endfor %}
                                {% if note.tags.size > 3 %}
                                    <span class="badge bg-light text-dark">+{{ note.tags.size | minus: 3 }}</span>
                                {% endif %}
                            {% endif %}
                        </div>
                    </div>
                </div>
            {% endfor %}
        </div>

        <!-- Empty State -->
        <div id="emptyState" class="text-center mt-5" style="display: none;">
            <h5>No notes found</h5>
            <p class="text-muted">Try adjusting your search or filter criteria.</p>
        </div>

        <!-- Stats -->
        <div class="mt-5 pt-4 border-top">
            <h4>Collection Overview</h4>
            <div class="row">
                <div class="col-md-6">
                    <h6>Categories</h6>
                    <ul class="list-unstyled">
                        {% for category in categories %}
                            {% assign category_count = site.notes | where: 'categories', category | size %}
                            <li>{{ category | capitalize }}: {{ category_count }} note{% if category_count != 1 %}s{% endif %}</li>
                        {% endfor %}
                    </ul>
                </div>
                <div class="col-md-6">
                    <h6>Popular Tags</h6>
                    <div>
                        {% assign tag_counts = '' | split: '' %}
                        {% for tag in tags %}
                            {% assign tag_count = site.notes | where_exp: "note", "note.tags contains tag" | size %}
                            {% assign tag_counts = tag_counts | push: tag_count %}
                        {% endfor %}
                        {% assign sorted_tags = tags | zip: tag_counts | sort: 1 | reverse %}
                        {% for tag_data in sorted_tags limit:10 %}
                            <span class="badge bg-outline-secondary me-1">{{ tag_data[0] }} ({{ tag_data[1] }})</span>
                        {% endfor %}
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>

<script>
// Search and filter functionality
document.addEventListener('DOMContentLoaded', function() {
    const searchInput = document.getElementById('noteSearch');
    const categoryFilter = document.getElementById('categoryFilter');
    const tagFilter = document.getElementById('tagFilter');
    const notesContainer = document.getElementById('notesContainer');
    const emptyState = document.getElementById('emptyState');
    const noteCards = document.querySelectorAll('.note-card');

    function filterNotes() {
        const searchTerm = searchInput.value.toLowerCase();
        const selectedCategory = categoryFilter.value.toLowerCase();
        const selectedTag = tagFilter.value.toLowerCase();
        
        let visibleCount = 0;

        noteCards.forEach(card => {
            const title = card.dataset.title;
            const content = card.dataset.content;
            const tags = card.dataset.tags;
            const categories = card.dataset.categories;

            const matchesSearch = !searchTerm || 
                title.includes(searchTerm) || 
                content.includes(searchTerm) || 
                tags.includes(searchTerm);
            
            const matchesCategory = !selectedCategory || categories.includes(selectedCategory);
            const matchesTag = !selectedTag || tags.includes(selectedTag);

            if (matchesSearch && matchesCategory && matchesTag) {
                card.style.display = 'block';
                visibleCount++;
            } else {
                card.style.display = 'none';
            }
        });

        // Show/hide empty state
        if (visibleCount === 0) {
            notesContainer.style.display = 'none';
            emptyState.style.display = 'block';
        } else {
            notesContainer.style.display = 'flex';
            emptyState.style.display = 'none';
        }
    }

    // Add event listeners
    searchInput.addEventListener('input', filterNotes);
    categoryFilter.addEventListener('change', filterNotes);
    tagFilter.addEventListener('change', filterNotes);
});
</script>