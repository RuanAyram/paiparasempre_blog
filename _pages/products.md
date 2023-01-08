---
title: Produtos
layout: page
permalink: "/produtos"
comments: false
---

<div class="alert alert-secondary">
	<h6 class="alert-heading" role="alert">Produtos recomendados pelo blog <u>Pai para sempre</u>.</h6>
	Essa não é uma página patrocinada. Contudo, o blog <strong>Pai para sempre</strong> pode receber uma comissão das lojas, caso você faça uma compra.
</div>

<div class="card-deck text-center">
  {% for produto in site.data.lista_produtos %}
    <div class="card border-primary" style="width: 18rem;">
      <a href="{{ produto.link }}" class="btn btn-primary">
        <img src="{{ site.baseurl }}/assets/images/logo_pai.png" class="card-img-top" alt="...">
      </a>
      <div class="card-body">
        <h5 class="card-title">{{ produto.nome }}</h5>
        <ul class="list-group list-group-flush">
          <li class="list-group-item">{{ produto.plataforma }}</li>
          <li class="list-group-item">R$ {{ produto.preco }}</li>
        </ul>
      </div>
      <div class="card-footer text-muted">
        <a href="{{ produto.link }}" class="btn btn-primary">Comprar</a>
      </div>
    </div>
  {% endfor %}
</div>

<div class="alert alert-secondary mt-3">
	<h6 class="alert-heading" role="alert">Produtos recomendados pelo blog <u>Pai para sempre</u>.</h6>
	Essa não é uma página patrocinada. Contudo, o blog <strong>Pai para sempre</strong> pode receber uma comissão das lojas, caso você faça uma compra.
</div>
