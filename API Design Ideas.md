<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>API Design Ideas</title>
  <link rel="stylesheet" href="https://stackedit.io/style.css" />
</head>

<body class="stackedit">
  <div class="stackedit__left">
    <div class="stackedit__toc">
      
<ul>
<li><a href="#api-design-ideas">API Design Ideas</a>
<ul>
<li></li>
</ul>
</li>
</ul>

    </div>
  </div>
  <div class="stackedit__right">
    <div class="stackedit__html">
      <h1 id="api-design-ideas">API Design Ideas</h1>
<hr>
<p>Date: 2018-10-29</p>
<h3 id="generic-gpu-buffer-mapping--other-buffers">Generic GPU Buffer Mapping &amp; Other Buffers</h3>
<pre class=" language-cpp"><code class="prism  language-cpp">BufferEntry <span class="token punctuation">{</span>
	U32 m_offset<span class="token punctuation">;</span>
	U32 m_size<span class="token punctuation">;</span>
	U32 m_maxSize<span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">;</span>

<span class="token comment">// A buffer that is on the GPU &amp; holds mappings of the data it stores</span>
GPUBuffer <span class="token punctuation">{</span>
<span class="token comment">// Size of the buffer</span>
U32 m_byteSize<span class="token punctuation">;</span>
<span class="token punctuation">}</span><span class="token punctuation">;</span>

<span class="token comment">// A buffer that is mapped between CPU &amp; GPU. Also, it holds mappings of the data it stores</span>
MappedGPUBuffer <span class="token operator">:</span> GPUBuffer <span class="token punctuation">{</span>
<span class="token comment">// Memory ptrs</span>
U8<span class="token operator">*</span> p_dataCur<span class="token punctuation">;</span>
U8<span class="token operator">*</span> p_dataBeg<span class="token punctuation">;</span>
U8<span class="token operator">*</span> p_dataEnd<span class="token punctuation">;</span>

<span class="token comment">// Entry storage</span>
Vector<span class="token operator">&lt;</span>BufferEntry<span class="token operator">&gt;</span> m_entries<span class="token punctuation">;</span>
<span class="token punctuation">}</span>

StructuredGPUBuffer <span class="token operator">:</span> GPUBuffer <span class="token punctuation">{</span>
<span class="token comment">// Stride of structured buffer</span>
U32 m_stride<span class="token punctuation">;</span>
<span class="token punctuation">}</span>

<span class="token comment">// APIs to write to MappedGPUBuffer, as they are the only ones available on CPU side</span>
<span class="token keyword">namespace</span> GPUBufferWriter <span class="token punctuation">{</span>
	U32 <span class="token function">AppendRaw</span><span class="token punctuation">(</span>MappedGPUBuffer<span class="token operator">&amp;</span> buffer<span class="token punctuation">,</span> <span class="token keyword">void</span><span class="token operator">*</span> data<span class="token punctuation">,</span> U32 byteSize<span class="token punctuation">,</span> U32 alignment<span class="token punctuation">,</span> <span class="token keyword">const</span> Log<span class="token operator">&amp;</span> log<span class="token punctuation">)</span><span class="token punctuation">;</span>
	U32 <span class="token function">AppendRaw</span><span class="token punctuation">(</span>MappedGPUBuffer<span class="token operator">&amp;</span> buffer<span class="token punctuation">,</span> U8<span class="token operator">*</span> data<span class="token punctuation">,</span> U32 byteSize<span class="token punctuation">,</span> U32 alignment<span class="token punctuation">,</span> <span class="token keyword">const</span> Log<span class="token operator">&amp;</span> log<span class="token punctuation">)</span><span class="token punctuation">;</span>
	<span class="token comment">// also maxSize extensions - That will allow us to reserve some space for data that changes but has a max limit to it.</span>

	U32 <span class="token function">AppendTexture</span><span class="token punctuation">(</span>MappedGPUBuffer<span class="token operator">&amp;</span> buffer<span class="token punctuation">,</span> U8<span class="token operator">*</span> data<span class="token punctuation">,</span> U32 byteSize<span class="token punctuation">,</span> U32 alignment<span class="token punctuation">,</span> U32 currentRowPitch<span class="token punctuation">,</span> U32 requiredRowPitch<span class="token punctuation">,</span> <span class="token keyword">const</span> Log<span class="token operator">&amp;</span> log<span class="token punctuation">)</span><span class="token punctuation">;</span>
	<span class="token comment">// also maxSize extensions - That will allow us to reserve some space for data that changes but has a max limit to it.</span>
<span class="token punctuation">}</span><span class="token punctuation">;</span>
</code></pre>
<p>A buffer that maps to the GPU and stores relevant buffer informations. (Like Constant Buffers, Structured Buffers, Textures etc.)</p>
<p>VkGPUBuffer and D3D12GPUBuffer are some relevant derivations that will hold other api specific information. Especially the process of creating such a buffer.</p>
<h3 id="descriptors--their-update-scope">Descriptors &amp; their update scope</h3>
<p>Certain descriptors could be:</p>
<ul>
<li>Renderer Level = Eg: Some UI Controls for the Sample</li>
<li>Pass Level = Eg: Some UI Controls for the Sample</li>
<li>Pool Level = A texture for the entire pool of drawables</li>
<li>Drawable Level (Only for Render Passes) = Eg: Model Matrix UniformBuffer</li>
</ul>
<p>We need a way to avoid duplicating the data if it is shared at a particular level.</p>
<p>Core things:</p>
<ul>
<li>Uniform Descriptor Heap for D3D12. Create a large pool outside. Not sure about Vulkan</li>
</ul>
<hr>

    </div>
  </div>
</body>

</html>
