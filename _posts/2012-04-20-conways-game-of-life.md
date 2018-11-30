---
layout: post
title: Conway's Game of Life
subtitle: in Javascript
bigimg: /img/daniel-falcao-418398-unsplash.png
tags: [software engineering]
---

In 2012 I worked for [Kuehne & Nagel](http://www.kn-portal.com/) in Hamburg. They do agile software development and follow "Clean Code". They invited me to take part on a company sponsored **code retreat** in April. So I stayed the weekend in Hamburg to hone my programming skills and to spend more time with my new coworkers. Thank you so much for this great opportunity!

[Here some background info on the code retreat format.](http://coderetreat.com/)

I never took a deeper look into [Conways Game of Life](http://en.wikipedia.org/wiki/Conway's_Game_of_Life) before, so I was astonished about how much complexity can emerge from such a small set of simple rules (think fractals).

At the Code Retreat we did TDD and pair programming with focus on different aspects such as small modules. Something I wanted to get going was to do TDD Javascript development. We used JsTestDriver for that and figured out how to do it.

On rule of a code retreat was to start each 45 min round from scratch with a new partner. So we could not finish the exercise. So the next day I completed the exercise with a running version.

[You can find my GoL Javascript code on github](https://github.com/markfink/GoL_Javascript)

<script type="text/javascript" src="/media/gol_code/GoL.js">
</script><script type="text/javascript">//<![CDATA[
	window.onload=function() {
	var cellSize = 8;
	var cellColor = '#FFFFFF';
	var activeCellColor = '#000080';
	var board = new gol.Board(40, 28);
	board.batch([[0, 2],[1, 0],[1, 2],[2, 1],[2, 2]]);
	var canvas = document.getElementById("golCanvas");
	board.run(canvas, cellSize, cellColor, activeCellColor);
	}
// ]]&gt;</script>
<canvas id="golCanvas" width="320" height="224" style="border: 1px solid #c3c3c3;">Your browser does not support the canvas element.</canvas>
