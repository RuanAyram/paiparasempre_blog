---
title: pages.products
layout: page

namespace: products

permalink: "/produtos"
permalink_en: "/products"
comments: false
---

<div class="alert alert-secondary">
	<h6 class="alert-heading" role="alert">Produtos recomendados pelo blog <u>Pai para sempre</u>.</h6>
	Essa não é uma página patrocinada. Contudo, o blog <strong>Pai para sempre</strong> pode receber uma comissão das lojas, caso você faça uma compra.
</div>

<div class="card-deck text-center">
  {% for produto in site.produtos %}
    {% include product.html %}
  {% endfor %}
</div>

<div class="alert alert-secondary mt-3">
	<h6 class="alert-heading" role="alert">Produtos recomendados pelo blog <u>Pai para sempre</u>.</h6>
	Essa não é uma página patrocinada. Contudo, o blog <strong>Pai para sempre</strong> pode receber uma comissão das lojas, caso você faça uma compra.
</div>
