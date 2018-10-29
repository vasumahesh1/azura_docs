API Design Ideas
===================

--------------

Date: 2018-10-29

Generic GPU Buffer Mapping & Other Buffers
--------------

```cpp
BufferEntry {
  U32 m_offset;
  U32 m_size;
  U32 m_maxSize;
};

// A buffer that is on the GPU & holds mappings of the data it stores
GPUBuffer {
  // Size of the buffer
  U32 m_byteSize;
};

// A buffer that is mapped between CPU & GPU. Also, it holds mappings of the data it stores
MappedGPUBuffer : GPUBuffer {
  // Memory ptrs
  U8* p_dataCur;
  U8* p_dataBeg;
  U8* p_dataEnd;

  // Entry storage
  Vector<BufferEntry> m_entries;
}

StructuredGPUBuffer : GPUBuffer {
  // Stride of structured buffer
  U32 m_stride;
}

// APIs to write to MappedGPUBuffer, as they are the only ones available on CPU side
namespace GPUBufferWriter {
  U32 AppendRaw(MappedGPUBuffer& buffer, void* data, U32 byteSize, U32 alignment, const Log& log);
  U32 AppendRaw(MappedGPUBuffer& buffer, U8* data, U32 byteSize, U32 alignment, const Log& log);
  // also maxSize extensions - That will allow us to reserve some space for data that changes but has a max limit to it.

  U32 AppendTexture(MappedGPUBuffer& buffer, U8* data, U32 byteSize, U32 alignment, U32 currentRowPitch, U32 requiredRowPitch, const Log& log);
  // also maxSize extensions - That will allow us to reserve some space for data that changes but has a max limit to it.
};
```

A buffer that maps to the GPU and stores relevant buffer informations. (Like Constant Buffers, Structured Buffers, Textures etc.)

VkGPUBuffer and D3D12GPUBuffer are some relevant derivations that will hold other api specific information. Especially the process of creating such a buffer.

Descriptors & their usage scope
--------------

Certain descriptors could be:
- Renderer Level = Eg: Some UI Controls for the Sample
- Pass Level = Eg: Some UI Controls for the Sample
- Pool Level = A texture for the entire pool of drawables
- Drawable Level (Only for Render Passes) = Eg: Model Matrix UniformBuffer

We need a way to avoid duplicating the data if it is shared at a particular level. This should be on a granularity of Descriptor Sets and not individual entries. 1 set has 1 place of update either at the renderer level, pass level (compute or render), pool level etc.

Pros:
- Already have a set for all types of descriptors added. Can maintain `UsageScope` there itself

Cons
- Issue comes with Renderer, Pass & Pools having similar ways of updating data & maintain 1 buffer for each level. But a drawable is actually sharing the buffer memory with the pool itself. So the pool has to maintain drawable buffer updates as well.

Notes / Foreseeable Changes:
- Uniform Descriptor Heap for D3D12. Create a large pool outside. Not sure about Vulkan.
- Need a governing structure which can be re-used among the different scopes and writes to relevant GPU bound buffers as needed.
- Render Passes might need a staging buffer as well for their scope specific updates.
- This certainly, for Vulkan, points to scope level descriptor sets & we write to those sets during Submit phase. And then, per drawable we generate a set of descriptors by "gathering" them from the renderer, render pass, pool. ComputePool might need a similar thing but no drawable scope level to worry about.





--------------



