

<script setup lang="ts">
import * as d3 from "d3";
import {forceData} from './mock'
console.log(d3);

const graph={

// Specify the chart’s dimensions.
const width = 928;
const height = 600;

// Compute the graph and start the force simulation.
const root = d3.hierarchy(forceData);
const links = root.links();
const nodes = root.descendants();

const simulation = d3.forceSimulation(nodes)
    .force("link", d3.forceLink(links).id(d => d.id).distance(0).strength(1))
    .force("charge", d3.forceManyBody().strength(-50))
    .force("x", d3.forceX())
    .force("y", d3.forceY());

// Create the container SVG.
const svg = d3.create("svg")
    .attr("width", width)
    .attr("height", height)
    .attr("viewBox", [-width / 2, -height / 2, width, height])
    .attr("style", "max-width: 100%; height: auto;");

// Append links.
const link = svg.append("g")
    .attr("stroke", "#999")
    .attr("stroke-opacity", 0.6)
  .selectAll("line")
  .forceData(links)
  .join("line");

// Append nodes.
const node = svg.append("g")
    .attr("fill", "#fff")
    .attr("stroke", "#000")
    .attr("stroke-width", 1.5)
  .selectAll("circle")
  .forceData(nodes)
  .join("circle")
    .attr("fill", d => d.children ? null : "#000")
    .attr("stroke", d => d.children ? null : "#fff")
    .attr("r", 3.5)
    .call(drag(simulation));

node.append("title")
    .text(d => d.forceData.name);

simulation.on("tick", () => {
  link
      .attr("x1", d => d.source.x)
      .attr("y1", d => d.source.y)
      .attr("x2", d => d.target.x)
      .attr("y2", d => d.target.y);

  node
      .attr("cx", d => d.x)
      .attr("cy", d => d.y);
});

invalidation.then(() => simulation.stop());

return svg.node();
}

</script>

<template>
    <div class="force-graph">


    </div>
</template>

<style scoped>
</style>
