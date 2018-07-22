---
layout: post
title: Build A Blog With Jekyll And GitHub Pages
categories: Note
tags: Blog Jekyll GitHub
comments: true
---

## What is Jekyll 


簡單的說, [Jekyll](http://jekyllrb.com) 是一個靜態網站的生成器, 很適合用來建立個人部落格或簡單商業網站, 而 Github Pages 也支援 Jekyll Theme, 即可以將你的網站部署到 Github 上進行託管, 如此一來你就可以專注在前端的維護及撰寫文章.

[Jekyll](http://jekyllrb.com) 提供強大和靈活性的功能, 可以幫助我們簡單又快速的建立一個網站, 且文章是採用 Markdwon 標準化語法, 通過簡單的標記語法，它可以使普通文本內容具有一定的格式. 
Find out more by [visiting the project on GitHub](https://github.com/mojombo/jekyll).

>Jekyll is a simple, blog-aware, static site generator perfect for personal, project, or organization sites. Think of it like a file-based CMS, without all the complexity. Jekyll takes your content, renders Markdown and Liquid templates, and spits out a complete, static website ready to be served by Apache, Nginx or another web server. Jekyll is the engine behind GitHub Pages, which you can use to host sites right from your GitHub repositories.

*--MORE--*

## Quick Start

### Step 1. Install Ruby and Bundler

To use Jekyll, we need Ruby.
First, Go to [Ruby](https://www.ruby-lang.org/en/downloads/) and download the installer for Ruby v2.3.1 that matches your system’s architecture (x86 / x64).

Then, run the command to install Bundler

	$ gem install bundler

### Step 2. Fork Jekyll to your User Repository

## Local Development

### Step 1. Clone down your fork

	$ git clone http://username.github.io/websitename yourLocalDirectory

### Step 2. Create Gemfile

	source 'https://rubygems.org'
	gem 'github-pages', group: :jekyll_plugins

### Step 3. Start Server

	$ cd directory
	$ bundle install
	$ bundle exec jekyll serve

Then, View your website at **http://127.0.0.1:4000/**
	

<table>
	<tr><td>_config.yml</td><td>The configuration settings for our site</td></tr>
	<tr><td>Gemfile</td><td> A list of Gem dependencies</td></tr>
	<tr><td>Gemfile.lock</td><td> A list of Gems AKA packages for your project</td></tr>
	<tr><td>_posts</td><td>Directory for blog posts</td></tr>
	<tr><td>_site</td><td>Directory where files are written</td></tr>
	<tr><td>404.html</td><td>Error page</td></tr>
	<tr><td>about.md</td><td>About page</td></tr>
	<tr><td>index.md</td><td>Home page</td></tr>
</table>
	


