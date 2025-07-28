---
layout: default
title: Home
---

<div class="row">
    <div class="col-lg-8 mx-auto">
        <div class="jumbotron bg-primary text-white p-5 rounded mb-4">
            <h1 class="display-4">Welcome to {{ site.title }}</h1>
            <p class="lead">{{ site.description }}</p>
            <hr class="my-4" style="border-color: rgba(255,255,255,0.3);">
            <p>This Jekyll site is powered by Bootstrap and ready for GitHub Pages.</p>
            <a class="btn btn-light btn-lg" href="#features" role="button">Learn more</a>
        </div>

        <section id="features" class="my-5">
            <h2>Features</h2>
            <div class="row">
                <div class="col-md-4 mb-3">
                    <div class="card h-100">
                        <div class="card-body">
                            <h5 class="card-title">Jekyll</h5>
                            <p class="card-text">Built with Jekyll, a simple, blog-aware, static site generator perfect for GitHub Pages.</p>
                        </div>
                    </div>
                </div>
                <div class="col-md-4 mb-3">
                    <div class="card h-100">
                        <div class="card-body">
                            <h5 class="card-title">Bootstrap</h5>
                            <p class="card-text">Styled with Bootstrap 5, providing responsive design and modern UI components.</p>
                        </div>
                    </div>
                </div>
                <div class="col-md-4 mb-3">
                    <div class="card h-100">
                        <div class="card-body">
                            <h5 class="card-title">Zettelkasten Notes</h5>
                            <p class="card-text">A collection of interconnected notes following the Zettelkasten method for knowledge management.</p>
                            <a href="{{ "/notes/" | relative_url }}" class="btn btn-primary">Browse Notes</a>
                        </div>
                    </div>
                </div>
            </div>
        </section>

        <section class="my-5">
            <h2>Getting Started</h2>
            <p>This site is built with minimal dependencies and uses CDN-hosted libraries for optimal performance:</p>
            <ul>
                <li><strong>Bootstrap CSS & JS</strong> - Loaded from jsDelivr CDN</li>
                <li><strong>Jekyll</strong> - Static site generation</li>
                <li><strong>GitHub Pages</strong> - Automatic deployment</li>
            </ul>
        </section>
    </div>
</div>