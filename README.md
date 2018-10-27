---
title: Azura Docs
author: Vasu Mahesh

---

<h1 id="azura">Azura</h1>
<p>A repository containing tools for real-time rendering, general C++, memory allocators, path tracers and more!</p>
<p>Active Platforms on Azura:</p>

<table>
<thead>
<tr>
<th>Windows</th>
<th align="center">Linux</th>
</tr>
</thead>
<tbody>
<tr>
<td><a href="https://ci.appveyor.com/project/vasumahesh1/azura"><img src="https://ci.appveyor.com/api/projects/status/github/vasumahesh1/azura" alt="Build Status: Windows"></a></td>
<td align="center">Soon™</td>
</tr>
</tbody>
</table><p>Active Draw APIs on Azura:</p>

<table>
<thead>
<tr>
<th align="center">D3D12</th>
<th align="center">Vulkan</th>
</tr>
</thead>
<tbody>
<tr>
<td align="center">Supported</td>
<td align="center">Supported</td>
</tr>
</tbody>
</table><p><img src="https://github.com/vasumahesh1/azura/raw/dev/Source/Samples/1_ProceduralPlanet/Images/planet_low.gif" alt=""></p>
<h1 id="table-of-contents">Table of Contents</h1>
<ul>
<li><a href="#dependencies">Dependencies</a></li>
<li><a href="#render-samples">Render Samples</a>
<ul>
<li><a href="#procedural-planet">Procedural Planet</a></li>
<li><a href="#forward-renderer">Forward+ Renderer</a></li>
</ul>
</li>
<li><a href="#projects">Projects</a>
<ul>
<li><a href="#render-system">Render System</a></li>
<li><a href="#memory-allocators">Memory Allocators</a></li>
<li><a href="#common">Common</a></li>
<li><a href="#Log">Log</a></li>
</ul>
</li>
<li><a href="#building">Building</a></li>
<li><a href="BENCHMARKS.md">Benchmarking</a></li>
<li><a href="#license">License</a></li>
</ul>
<h1 id="dependencies">Dependencies</h1>
<p>Build time dependencies:</p>
<ul>
<li><a href="https://cmake.org/">CMake (3.11 or above)</a></li>
<li><a href="https://ninja-build.org/">Ninja</a></li>
</ul>
<p>Test / Code Sanity dependencies:</p>
<ul>
<li><a href="https://github.com/google/googletest">Google Test</a></li>
<li><a href="https://github.com/google/benchmark">Google Benchmark</a></li>
<li><a href="https://llvm.org/">Clang-tidy (LLVM)</a></li>
</ul>
<p>Code dependencies:</p>
<ul>
<li><a href="https://github.com/jbeder/yaml-cpp">yaml-cpp</a></li>
<li><a href="https://www.boost.org/">boost</a></li>
<li><a href="https://github.com/google/mathfu">mathfu</a></li>
<li><a href="https://www.lunarg.com/vulkan-sdk/">Vulkan SDK</a></li>
<li><a href="https://www.glfw.org/">GLFW</a></li>
<li><a href="https://github.com/Microsoft/glTF-SDK">GLTF SDK</a></li>
</ul>
<p>Most of the dependencies are located at Source/Imports/ and are pulled automatically using git submodule. If you cloned this repository, you can run:</p>
<pre><code>git submodule update --init --recursive
</code></pre>
<p>This will download most of the code dependencies.</p>
<h1 id="render-samples">Render Samples</h1>
<h2 id="procedural-planet">Procedural Planet</h2>
<p><img src="https://github.com/vasumahesh1/azura/raw/master/Source/Samples/1_ProceduralPlanet/Images/planet_low.gif" alt=""></p>

<table>
<thead>
<tr>
<th align="center">D3D12</th>
<th align="center">Vulkan</th>
</tr>
</thead>
<tbody>
<tr>
<td align="center">Supported</td>
<td align="center">Supported</td>
</tr>
</tbody>
</table><h4 id="project-features">Project features</h4>
<ul>
<li>Traditional Deferred Pipeline</li>
<li>3 G-Buffers - Positional / UV &amp; Terrain Elevation / Normals</li>
<li>Multiple Passes - Noise Pass &amp; Sky Pass --&gt; Terrain Pass --&gt; Water Pass</li>
</ul>

<table>
<thead>
<tr>
<th align="center">GBuffer 1</th>
<th align="center">GBuffer 2</th>
<th align="center">GBuffer 3</th>
</tr>
</thead>
<tbody>
<tr>
<td align="center"><img src="https://github.com/vasumahesh1/azura/raw/master/Source/Samples/1_ProceduralPlanet/Images/frame_position.PNG" alt=""></td>
<td align="center"><img src="https://github.com/vasumahesh1/azura/raw/master/Source/Samples/1_ProceduralPlanet/Images/frame_normal.PNG" alt=""></td>
<td align="center"><img src="https://github.com/vasumahesh1/azura/raw/master/Source/Samples/1_ProceduralPlanet/Images/frame_uv_elevation.PNG" alt=""></td>
</tr>
</tbody>
</table>
<table>
<thead>
<tr>
<th align="center">Final Frame</th>
</tr>
</thead>
<tbody>
<tr>
<td align="center"><img src="https://github.com/vasumahesh1/azura/raw/master/Source/Samples/1_ProceduralPlanet/Images/frame_main.PNG" alt=""></td>
</tr>
</tbody>
</table><h2 id="forward-renderer">Forward+ Renderer</h2>
<p><img src="https://github.com/vasumahesh1/azura/raw/master/Source/Samples/2_DeferredRenderer/Images/sponza_1_low.gif" alt=""></p>

<table>
<thead>
<tr>
<th align="center">D3D12</th>
<th align="center">Vulkan</th>
</tr>
</thead>
<tbody>
<tr>
<td align="center">Supported</td>
<td align="center">Not Supported*</td>
</tr>
</tbody>
</table><p>*Not supported due to missing <code>ComputePool</code> &amp; <code>ComputePass</code> implementation for Vulkan. Based on the timeline, Support will be added as soon as possible. <a href="https://github.com/vasumahesh1/azura/issues/34">Issue #34</a> tracks this pending feature.</p>
<h3 id="frame-debug-views">Frame Debug Views</h3>

<table>
<thead>
<tr>
<th align="center">Albedo</th>
<th align="center">Normals</th>
<th align="center">Depth</th>
</tr>
</thead>
<tbody>
<tr>
<td align="center"><img src="https://github.com/vasumahesh1/azura/raw/master/Source/Samples/2_DeferredRenderer/Images/frame_albedo.PNG" alt=""></td>
<td align="center"><img src="https://github.com/vasumahesh1/azura/raw/master/Source/Samples/2_DeferredRenderer/Images/frame_normals.PNG" alt=""></td>
<td align="center"><img src="https://github.com/vasumahesh1/azura/raw/master/Source/Samples/2_DeferredRenderer/Images/frame_depth.PNG" alt=""></td>
</tr>
</tbody>
</table><h3 id="pipeline-structure">Pipeline Structure</h3>
<div class="mermaid"><svg xmlns="http://www.w3.org/2000/svg" id="mermaid-svg-Xj5c1vEas8juyHMe" width="100%" style="max-width: 473.59375px;" viewBox="0 0 473.59375 62"><g transform="translate(-12, -12)"><g class="output"><g class="clusters"></g><g class="edgePaths"><g class="edgePath" style="opacity: 1;"><path class="path" d="M146.796875,43L171.796875,43L196.796875,43" marker-end="url(#arrowhead12816)" style="fill:none"></path><defs><marker id="arrowhead12816" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath" style="opacity: 1;"><path class="path" d="M316.859375,43L341.859375,43L366.859375,43" marker-end="url(#arrowhead12817)" style="fill:none"></path><defs><marker id="arrowhead12817" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g></g><g class="edgeLabels"><g class="edgeLabel" transform="" style="opacity: 1;"><g transform="translate(0,0)" class="label"><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span class="edgeLabel"></span></div></foreignObject></g></g><g class="edgeLabel" transform="" style="opacity: 1;"><g transform="translate(0,0)" class="label"><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span class="edgeLabel"></span></div></foreignObject></g></g></g><g class="nodes"><g class="node" id="A" transform="translate(83.3984375,43)" style="opacity: 1;"><rect rx="0" ry="0" x="-63.3984375" y="-23" width="126.796875" height="46"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-53.3984375,-13)"><foreignObject width="106.796875" height="26"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">Depth Pre Pass</div></foreignObject></g></g></g><g class="node" id="B" transform="translate(256.828125,43)" style="opacity: 1;"><rect rx="0" ry="0" x="-60.03125" y="-23" width="120.0625" height="46"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-50.03125,-13)"><foreignObject width="100.0625" height="26"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">Compute Pass</div></foreignObject></g></g></g><g class="node" id="C" transform="translate(422.2265625,43)" style="opacity: 1;"><rect rx="0" ry="0" x="-55.3671875" y="-23" width="110.734375" height="46"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-45.3671875,-13)"><foreignObject width="90.734375" height="26"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">Shading Pass</div></foreignObject></g></g></g></g></g></g></svg></div>
<p><strong>Data uploaded only once to GPU:</strong></p>
<ul>
<li>
<p>Tile Frustums<br>
We upload only the pre-computed frustums as a StructuredBuffer so we don’t spend time getting each ThreadGroup’s 4 frustums.</p>
</li>
<li>
<p>Initial Light Texture</p>
</li>
</ul>
<hr>
<p><strong>Pass Information:</strong></p>
<ul>
<li>
<p>Depth Pre Pass<br>
Regular depth pass no other computation.</p>
</li>
<li>
<p>Compute Pass</p>
<ul>
<li>Launch 1 ThreadGroup for 1 Tile; For best results threads per group was 256</li>
</ul>
<div class="mermaid"><svg xmlns="http://www.w3.org/2000/svg" id="mermaid-svg-ow31ogcDkrFZaW8V" width="100%" style="max-width: 436.46875px;" viewBox="0 0 436.46875 734"><g transform="translate(-12, -12)"><g class="output"><g class="clusters"></g><g class="edgePaths"><g class="edgePath" style="opacity: 1;"><path class="path" d="M230.234375,66L230.234375,91L230.234375,116" marker-end="url(#arrowhead12854)" style="fill:none"></path><defs><marker id="arrowhead12854" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath" style="opacity: 1;"><path class="path" d="M230.234375,162L230.234375,187L230.234375,212" marker-end="url(#arrowhead12855)" style="fill:none"></path><defs><marker id="arrowhead12855" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath" style="opacity: 1;"><path class="path" d="M230.234375,258L230.234375,283L230.234375,308" marker-end="url(#arrowhead12856)" style="fill:none"></path><defs><marker id="arrowhead12856" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath" style="opacity: 1;"><path class="path" d="M230.234375,354L230.234375,379L230.234375,404" marker-end="url(#arrowhead12857)" style="fill:none"></path><defs><marker id="arrowhead12857" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath" style="opacity: 1;"><path class="path" d="M230.234375,450L230.234375,475L230.234375,500" marker-end="url(#arrowhead12858)" style="fill:none"></path><defs><marker id="arrowhead12858" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath" style="opacity: 1;"><path class="path" d="M230.234375,546L230.234375,571L230.234375,596" marker-end="url(#arrowhead12859)" style="fill:none"></path><defs><marker id="arrowhead12859" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g><g class="edgePath" style="opacity: 1;"><path class="path" d="M230.234375,642L230.234375,667L230.234375,692" marker-end="url(#arrowhead12860)" style="fill:none"></path><defs><marker id="arrowhead12860" viewBox="0 0 10 10" refX="9" refY="5" markerUnits="strokeWidth" markerWidth="8" markerHeight="6" orient="auto"><path d="M 0 0 L 10 5 L 0 10 z" class="arrowheadPath" style="stroke-width: 1; stroke-dasharray: 1, 0;"></path></marker></defs></g></g><g class="edgeLabels"><g class="edgeLabel" transform="" style="opacity: 1;"><g transform="translate(0,0)" class="label"><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span class="edgeLabel"></span></div></foreignObject></g></g><g class="edgeLabel" transform="" style="opacity: 1;"><g transform="translate(0,0)" class="label"><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span class="edgeLabel"></span></div></foreignObject></g></g><g class="edgeLabel" transform="" style="opacity: 1;"><g transform="translate(0,0)" class="label"><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span class="edgeLabel"></span></div></foreignObject></g></g><g class="edgeLabel" transform="" style="opacity: 1;"><g transform="translate(0,0)" class="label"><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span class="edgeLabel"></span></div></foreignObject></g></g><g class="edgeLabel" transform="" style="opacity: 1;"><g transform="translate(0,0)" class="label"><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span class="edgeLabel"></span></div></foreignObject></g></g><g class="edgeLabel" transform="" style="opacity: 1;"><g transform="translate(0,0)" class="label"><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span class="edgeLabel"></span></div></foreignObject></g></g><g class="edgeLabel" transform="" style="opacity: 1;"><g transform="translate(0,0)" class="label"><foreignObject width="0" height="0"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;"><span class="edgeLabel"></span></div></foreignObject></g></g></g><g class="nodes"><g class="node" id="A" transform="translate(230.234375,43)" style="opacity: 1;"><rect rx="0" ry="0" x="-62.40625" y="-23" width="124.8125" height="46"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-52.40625,-13)"><foreignObject width="104.8125" height="26"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">Animate Lights</div></foreignObject></g></g></g><g class="node" id="B" transform="translate(230.234375,235)" style="opacity: 1;"><rect rx="0" ry="0" x="-134.4921875" y="-23" width="268.984375" height="46"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-124.4921875,-13)"><foreignObject width="248.984375" height="26"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">Compute Atomic Min &amp; Max Depth</div></foreignObject></g></g></g><g class="node" id="C" transform="translate(230.234375,427)" style="opacity: 1;"><rect rx="0" ry="0" x="-153.1484375" y="-23" width="306.296875" height="46"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-143.1484375,-13)"><foreignObject width="286.296875" height="26"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">Per ThreadGroup - Iterate through Lights</div></foreignObject></g></g></g><g class="node" id="D" transform="translate(230.234375,715)" style="opacity: 1;"><rect rx="0" ry="0" x="-209.4765625" y="-23" width="418.953125" height="46"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-199.4765625,-13)"><foreignObject width="398.953125" height="26"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">Per ThreadGroup - Write Active Lights to Cluster Texture</div></foreignObject></g></g></g><g class="node" id="W" transform="translate(230.234375,619)" style="opacity: 1;"><rect rx="5" ry="5" x="-33.96875" y="-23" width="67.9375" height="46"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-23.96875,-13)"><foreignObject width="47.9375" height="26"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">Barrier</div></foreignObject></g></g></g><g class="node" id="X" transform="translate(230.234375,139)" style="opacity: 1;"><rect rx="5" ry="5" x="-33.96875" y="-23" width="67.9375" height="46"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-23.96875,-13)"><foreignObject width="47.9375" height="26"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">Barrier</div></foreignObject></g></g></g><g class="node" id="Y" transform="translate(230.234375,331)" style="opacity: 1;"><rect rx="5" ry="5" x="-33.96875" y="-23" width="67.9375" height="46"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-23.96875,-13)"><foreignObject width="47.9375" height="26"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">Barrier</div></foreignObject></g></g></g><g class="node" id="Z" transform="translate(230.234375,523)" style="opacity: 1;"><rect rx="5" ry="5" x="-210.234375" y="-23" width="420.46875" height="46"></rect><g class="label" transform="translate(0,0)"><g transform="translate(-200.234375,-13)"><foreignObject width="400.46875" height="26"><div xmlns="http://www.w3.org/1999/xhtml" style="display: inline-block; white-space: nowrap;">Per ThreadGroup - Atomic Append to Active Lights Array</div></foreignObject></g></g></g></g></g></g></svg></div>
</li>
<li>
<p>Shading Pass</p>
<ul>
<li>Read from above Cluster Texture &amp; Shade</li>
</ul>
</li>
</ul>
<hr>
<h3 id="nsight-debug-views">NSight Debug Views</h3>

<table>
<thead>
<tr>
<th align="center">Light Texture</th>
<th align="center">Cluster Texture</th>
</tr>
</thead>
<tbody>
<tr>
<td align="center"><img src="https://github.com/vasumahesh1/azura/raw/master/Source/Samples/2_DeferredRenderer/Images/light_texture.PNG" alt=""></td>
<td align="center"><img src="https://github.com/vasumahesh1/azura/raw/master/Source/Samples/2_DeferredRenderer/Images/cluster_texture.PNG" alt=""></td>
</tr>
</tbody>
</table>
<table>
<thead>
<tr>
<th align="center">Final Frame</th>
</tr>
</thead>
<tbody>
<tr>
<td align="center"><img src="https://github.com/vasumahesh1/azura/raw/master/Source/Samples/2_DeferredRenderer/Images/frame_main.PNG" alt=""></td>
</tr>
</tbody>
</table><h4 id="references">References</h4>
<ul>
<li><a href="https://takahiroharada.files.wordpress.com/2015/04/forward_plus.pdf">Original Paper on Forward+ Rendering by Harada et. al</a></li>
<li><a href="https://www.ea.com/frostbite/news/directx-11-rendering-in-battlefield-3">EA Battlefield 3 - GDC Slides for Forward+ Rendering</a></li>
</ul>
<h1 id="building">Building</h1>
<h2 id="tldr">TLDR</h2>
<p>if you want to just do a simple build:</p>
<pre><code>python build.py --project all --target Win64
</code></pre>
<h2 id="all-options">All Options</h2>
<p>Building Azura may seem complicated but it is essentially 1 python script doing all the magic. Here is a list of options available to the user:</p>
<pre class=" language-bash"><code class="prism  language-bash">usage: build.py <span class="token punctuation">[</span>-h<span class="token punctuation">]</span> <span class="token punctuation">[</span>--project PROJECT<span class="token punctuation">]</span> --target TARGET
                <span class="token punctuation">[</span>--generator GENERATOR<span class="token punctuation">]</span> <span class="token punctuation">[</span>--configFile CONFIGFILE<span class="token punctuation">]</span>
                <span class="token punctuation">[</span>--cmakeConfigFile CMAKECONFIGFILE<span class="token punctuation">]</span>
                <span class="token punctuation">[</span>--projectGenerator PROJECTGENERATOR<span class="token punctuation">]</span> <span class="token punctuation">[</span>--buildPath BUILDPATH<span class="token punctuation">]</span>
                <span class="token punctuation">[</span>--projectPath PROJECTPATH<span class="token punctuation">]</span> <span class="token punctuation">[</span>--verbose<span class="token punctuation">]</span> <span class="token punctuation">[</span>--debug<span class="token punctuation">]</span> <span class="token punctuation">[</span>--clean<span class="token punctuation">]</span>
                <span class="token punctuation">[</span>--build BUILD<span class="token punctuation">]</span> <span class="token punctuation">[</span>--projectFiles<span class="token punctuation">]</span> <span class="token punctuation">[</span>--includeTests<span class="token punctuation">]</span> <span class="token punctuation">[</span>-v<span class="token punctuation">]</span>

optional arguments:
  -h, --help            show this <span class="token function">help</span> message and <span class="token keyword">exit</span>

  --project PROJECT     Project to build

  --target TARGET       Project to build on

  --generator GENERATOR
                        CMake Generator

  --configFile CONFIGFILE
                        Config File Override

  --cmakeConfigFile CMAKECONFIGFILE
                        CMake Config File Override

  --projectGenerator PROJECTGENERATOR
                        CMake Project Files Generator
  
  --buildPath BUILDPATH
                        Build Path
  
  --projectPath PROJECTPATH
                        Projects Path
  
  --verbose             Verbose Mode
  
  --debug               Debug Commands Mode
  
  --clean               Clean the project
  
  --build BUILD         Build Release or Debug, defaults to Debug Mode
  
  --projectFiles        Flag to tell the build system to generate project
                        files
  
  --includeTests        Flag to run tests as well
  
  -v                    Version

</code></pre>
<p>It is highly customizable and uses <code>.ini</code> files to change configs. For example, the difference between Appveyor and my current local repository is 1 .ini file.</p>
<h2 id="custom-cmake-overrides">Custom CMake Overrides</h2>
<p>There are two important config (.ini) files that you can provide to Azura build system.</p>
<pre><code>--configFile CONFIGFILE
                        Config File Override

--cmakeConfigFile CMAKECONFIGFILE
                        CMake Config File Override
</code></pre>
<ul>
<li>
<p><strong>–configFile</strong></p>
<p>Config File is your Environment Config.</p>
<pre><code>[Windows]
CMake=Tools/CMake/cmake-3.11.4-win64-x64/bin/
Ninja=Tools/Ninja/
LLVM=Tools/LLVM/x64/LLVM/bin/
VSBuildTools=VisualStudioBuildTools/
MSVCPath=VisualStudioBuildTools/VC/Tools/MSVC/14.14.26428/
Windows10SDKLib=Windows Kits/10/Lib/10.0.17134.0/
Windows10SDKBin=Windows Kits/10/bin/10.0.17134.0/
Windows10SDKInc=Windows Kits/10/Include/10.0.17134.0/

[Linux]
...

[MacOS]
...
</code></pre>
<p>If you have custom locations for these above files, you can make a custom ini file and tell Azura to use it. Appveyor basically has its own config located <a href="https://github.com/vasumahesh1/azura/blob/master/External/AppveyorConfig.ini">here</a>.</p>
</li>
<li>
<p><strong>–cmakeConfigFile</strong></p>
<p>These are custom CMake Overrides. Here, you can define custom variables that you want. Appveyor for example already has boost, so we just point boost to the correct place and we are done!</p>
<pre><code>[Defines]
VULKAN_1_1_77_0_ROOT=C:/AppveyorCache/VulkanSDK/1.1.77.0/
BOOST_ROOT=C:/Libraries/boost_1_67_0
GLFW_3_2_1_32_ROOT=C:/AppveyorCache/GLFW/glfw-3.2.1.bin.WIN32/
GLFW_3_2_1_64_ROOT=C:/AppveyorCache/GLFW/glfw-3.2.1.bin.WIN64/
</code></pre>
<p>You can also build private repositories:</p>
<pre><code>FORCE_INCLUDE_SUB_DIRECTORIES=Sandbox;MyCustomPrivateRepo
</code></pre>
</li>
</ul>
<h1 id="misc">Misc</h1>
<p>Some pseudo APIs I work on before implementing it on Azura:<br>
<a href="https://gist.github.com/vasumahesh1/08fa44f16daba245574794e18ebd47dd">Design Gist Link</a></p>
<h1 id="license">License</h1>
<p>Copyright 2018 Vasu Mahesh</p>
<p>Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the “Software”), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:</p>
<p>The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.</p>
<p>THE SOFTWARE IS PROVIDED “AS IS”, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.</p>

