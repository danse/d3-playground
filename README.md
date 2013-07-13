
This is a super simple html page made in order to play with d3 selections

# start

[Load the page directly](http://danse.github.io/d3-playground/) or download the
repo. The page is empty, it's intended to be used from the console

# scaring snakes

Snakes and programming come together. Ask python programmers. Animating a
visualization from the console will result in a long one-shot console command.
For someone, this could be a funny way to experiment.

My advice is to try from scratch and then compare with the working snakes.

Those oneliners will look broken on github, but with double-click (or any way
you use on your system in order to select a row) you can anyway copy-paste them
correctly on the console.

**Disclaimer**: this is not, at any extent, a good practice while writing d3
code. It's terrible! It's just an alternative way for learning.

## a basic one

Here it is an example of scaring script you can run from the console in this
page. It will animate some divs, and it offers you high flexibility in the
transition for the different selections.

``
d3.select('body').selectAll('.box').data(random(), function(d){return d.city;}).call(function(s){s.style('border', '1px solid black').transition().duration(duration).style('top', function(d, i){return 50+i*30;}).transition().duration(2*duration).style('width', function(d){ return d.value*200; });}).call(function(s){s.enter().append('div').attr('class', 'box').text(function(d){return d.city;}).style('top', function(d, i){return 50+i*30;}).transition().duration(duration).delay().style('width', function(d){return d.value*200;});}).call(function(s){s.exit().transition().duration(duration).style('top', 2000).remove();})
``

This snake is available, translated in a sane version, in the `update` method
in the `sane.html` file.

## slightly better

The snake can be shortened merging the enter and create selection, although
this way there is no flexibility in specifying different behaviors for the two
selections.

``
d3.select('body').selectAll('.box').data(random(), function(d){return d.city;}).call(function(s){s.enter().append('div').attr('class', 'box').text(function(d){return d.city;})}).call(function(s){s.style('border', '1px solid black').transition().duration(duration).style('top', function(d, i){return 50+i*30;}).transition().duration(2*duration).style('width', function(d){ return d.value*200; });}).call(function(s){s.exit().transition().duration(duration).style('top', 2000).remove();})
``

## the vectorial snake

``
d3.select('svg').selectAll('.box').data(random(), function(d){return d.city;}).call(function(s){ var g = s.enter().append('g').attr('class', 'box'); g.append('rect').attr('height', 18);; g.append('text').attr('y', 15).text(function(d){ return d.city; })}).call(function(s){s.transition().duration(duration).attr('transform', function(d, i){ return 'translate(10, '+i * 20+')'; }).select('rect').attr('width', function(d){ return d.value * 100; })}).call(function(s){s.exit().transition().duration(duration).attr('transform', 'translate(10, 2000)').remove();})
``

## a word snake

How would it be to play with an existing text with d3? the `words.html` is
slightly modified to help for this, and the corresponding "snake" is the
following

``
d3.select('.text').selectAll('span').data(random(words), function(d){return d ? d.label : d3.select(this).text().trim();}).call(function(s){s.enter().append('span').text(function(d){return d.label+' ';}).transition().duration(duration).style('opacity', 1);}).call(function(s){ s.exit().transition().duration(duration).style('opacity', 0).remove()})
``

Where a little trick helps to have a valid key value also for elements
preexisting in the page, not generated with d3.
