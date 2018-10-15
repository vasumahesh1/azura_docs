---
title: Azura Docs
author: Vasu Mahesh

---

<h1 id="azura">Azura</h1>
<p>A repository containing tools for real-time rendering, general C++, memory allocators, path tracers and more!</p>
<p>Note: This is still a WIP and very much an active project.</p>

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
</table><h1 id="table-of-contents">Table of Contents</h1>
<ul>
<li><a href="#dependencies">Dependencies</a></li>
<li><a href="#building">Building</a></li>
<li><a href="#projects">Projects</a>
<ul>
<li><a href="#render-system">Render System</a></li>
<li><a href="#common">Common</a></li>
<li><a href="#Log">Log</a></li>
</ul>
</li>
<li><a href="#renders">Renders</a></li>
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
</ul>
<p>Most of the dependencies are located at Source/Imports/ and are pulled automatically using git submodule. If you cloned this repository, you can run:</p>
<pre><code>git submodule update --init --recursive
</code></pre>
<p>This will download most of the code dependencies.</p>
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

