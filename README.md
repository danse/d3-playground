
This is a super simple html page made to play with d3

# start

[Load the page directly]() or download the repo. The page is empty, it's intended
to be used from the console

# scaring snakes

Snakes and programming come together. Ask python programmers. Animating a
visualization from the console will result in a long one-shot console command.
For someone, this could be a funny way to experiment.

## a basic one

Here it is an example of scaring script you can run from the console in this
page

``
d3.select('body').selectAll('.box').data(random(), function(d){return d.city;}).call(function(s){s.style('border', '1px solid black').transition().duration(duration).style('top', function(d, i){return 50+i*30;}).transition().duration(2*duration).style('width', function(d){ return d.value*200; });}).call(function(s){s.enter().append('div').attr('class', 'box').text(function(d){return d.city;}).style('top', function(d, i){return 50+i*30;}).transition().duration(duration).delay().style('width', function(d){return d.value*200;});}).call(function(s){s.exit().transition().duration(duration).style('top', 2000).remove();})
``

## slightly better

The snake can be shortened merging the enter and create selection, although
this way there is no flexibility in specifying different behaviors for the two
selections

``
d3.select('body').selectAll('.box').data(random(), function(d){return d.city;}).call(function(s){s.enter().append('div').attr('class', 'box').text(function(d){return d.city;})}).call(function(s){s.style('border', '1px solid black').transition().duration(duration).style('top', function(d, i){return 50+i*30;}).transition().duration(2*duration).style('width', function(d){ return d.value*200; });}).call(function(s){s.exit().transition().duration(duration).style('top', 2000).remove();})
``

## the vectorial snake

``
d3.select('svg').selectAll('.box').data(random(), function(d){return d.city;}).call(function(s){s.style('border', '1px solid black').transition().duration(duration).attr('y', function(d, i){return 50+i*30;}).transition().duration(2*duration).attr('width', function(d){ return d.value*200; });}).call(function(s){s.enter().append('rect').attr('class', 'box').attr('height', 30).text(function(d){return d.city;}).attr('y', function(d, i){return 50+i*30;}).transition().duration(duration).delay().attr('width', function(d){return d.value*200;});}).call(function(s){s.exit().transition().duration(duration).attr('y', 2000).remove();})
``
