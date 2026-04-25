# KINA SAQINA — 绮娜·萨琪娜 角色展示页面

> **BITNP: Net Pioneer Association of BIT**

---

## 📋 项目概述

本项目是 **Kina SaQina（绮娜·萨琪娜）** 角色展示页面，使用现代前端技术栈构建。
页面设计灵感来源于日系角色介绍卡片风格，包含：

- 🎨 带有斜线纹理（arsir/hatching）效果的大号水印文字
- 🏷️ 角色属性标签系统（阵营、种族、语言等）
- 🎯 黄色色块 + 白色主区域的分区布局
- 🦶 深色页脚 + 组织品牌信息
- 🔲 3D 模型展示区域（预留，使用 Three.js）
- ✨ GSAP 动画框架（已安装，待集成）

---

## 🛠️ 技术栈

| 技术 | 版本 | 用途 |
|------|------|------|
| **Vue 3** | ^3.5 | 前端框架（Composition API） |
| **Vite** | ^8.0 | 构建工具和开发服务器 |
| **TypeScript** | ~6.0 | 类型安全 |
| **SCSS (Sass)** | latest | 样式预处理器 |
| **GSAP** | latest | 高性能动画库 |
| **Three.js** | latest | 3D 渲染引擎 |

---

## 📁 项目结构

```
big-project/
├── index.html              # 入口 HTML（含 Google Fonts）
├── package.json            # 项目依赖配置
├── vite.config.ts          # Vite 构建配置
├── tsconfig.json           # TypeScript 配置
├── src/
│   ├── main.ts             # 应用入口
│   ├── style.scss          # 全局 SCSS 样式（设计令牌）
│   ├── App.vue             # 根组件
│   ├── assets/             # 静态资源
│   └── components/
│       └── BerryChanPage.vue  # 主页面组件（Kina SaQina）
└── public/                 # 公共静态文件
```

---

## 🚀 快速开始

```bash
# 安装依赖
npm install

# 启动开发服务器
npm run dev

# 构建生产版本
npm run build
```

---

## 🎬 GSAP 使用文档

### 什么是 GSAP？

**GSAP（GreenSock Animation Platform）** 是一个专业级的 JavaScript 动画库。
它比 CSS 动画更强大、更灵活，支持复杂的时间轴动画和滚动触发。

### 安装状态

```json
// package.json 中已安装
"gsap": "latest"
```

### 基础用法 — 在 Vue 3 中使用 GSAP

#### 1. 导入 GSAP

```typescript
// 在 Vue 组件的 <script setup> 中
import { onMounted, ref } from 'vue'
import gsap from 'gsap'
```

#### 2. 基本动画

```typescript
// 元素淡入 + 上移动画
onMounted(() => {
  gsap.from('.hero__watermark', {
    opacity: 0,
    y: 50,
    duration: 1.2,
    ease: 'power3.out'
  })
})
```

#### 3. 时间轴动画（Timeline）

```typescript
onMounted(() => {
  const tl = gsap.timeline({ defaults: { ease: 'power2.out' } })

  tl.from('.info-card', {
    opacity: 0,
    x: -30,
    duration: 0.8
  })
  .from('.hero__watermark', {
    opacity: 0,
    scale: 0.9,
    duration: 1
  }, '-=0.4')  // 重叠 0.4 秒
  .from('.tags .tag-group', {
    opacity: 0,
    y: 20,
    stagger: 0.15,  // 每个标签间隔 0.15 秒
    duration: 0.6
  }, '-=0.3')
})
```

#### 4. 滚动触发动画（ScrollTrigger）

```typescript
import gsap from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

// 注册插件
gsap.registerPlugin(ScrollTrigger)

onMounted(() => {
  gsap.from('.profile__desc', {
    scrollTrigger: {
      trigger: '.profile__desc',
      start: 'top 80%',    // 元素顶部到达视口 80% 位置时开始
      end: 'bottom 20%',
      toggleActions: 'play none none reverse'
    },
    opacity: 0,
    y: 40,
    duration: 0.8
  })
})
```

#### 5. 本项目推荐的动画方案

```typescript
// 在 BerryChanPage.vue 中实现的推荐动画
import { onMounted } from 'vue'
import gsap from 'gsap'

onMounted(() => {
  const tl = gsap.timeline({
    defaults: { ease: 'power3.out', duration: 0.8 }
  })

  // 1. 页面进入 - 黄色色块滑入
  tl.from('.hero__yellow-block', {
    scaleX: 0,
    transformOrigin: 'right center',
    duration: 1
  })

  // 2. 信息卡片淡入
  .from('.info-card', {
    opacity: 0,
    x: -40,
    duration: 0.6
  }, '-=0.5')

  // 3. 水印文字逐渐显现
  .from('.hero__watermark', {
    opacity: 0,
    x: -60,
    duration: 1.2,
    ease: 'power4.out'
  }, '-=0.4')

  // 4. 角色名称
  .from('.profile__name-row', {
    opacity: 0,
    y: 20
  }, '-=0.3')

  // 5. 标签依次出现
  .from('.tag-group', {
    opacity: 0,
    x: -20,
    stagger: 0.1
  }, '-=0.2')

  // 6. 青色线条展开
  .from('.teal-line', {
    scaleX: 0,
    transformOrigin: 'left center',
    duration: 0.6
  }, '-=0.2')

  // 7. 描述文字
  .from('.profile__desc p', {
    opacity: 0,
    y: 15,
    stagger: 0.15
  }, '-=0.2')

  // 8. 页脚
  .from('.footer', {
    opacity: 0,
    y: 30
  }, '-=0.1')
})
```

### GSAP 常用 Ease 曲线

| 名称 | 效果 | 适用场景 |
|------|------|----------|
| `power1.out` | 轻微减速 | 普通元素移动 |
| `power2.out` | 中等减速 | 卡片、面板出现 |
| `power3.out` | 强烈减速 | 大号文字、英雄区 |
| `power4.out` | 极强减速 | 水印、大型元素 |
| `elastic.out` | 弹性效果 | 按钮、图标弹入 |
| `back.out` | 回弹效果 | 菜单项、标签 |
| `expo.out` | 指数减速 | 全屏过渡 |

### GSAP 关键 API

```typescript
// ── 基本方法 ──
gsap.to(target, vars)      // 从当前状态动画到目标状态
gsap.from(target, vars)    // 从目标状态动画到当前状态
gsap.fromTo(target, fromVars, toVars)  // 指定起止状态
gsap.set(target, vars)     // 立即设置属性（无动画）

// ── 时间轴 ──
const tl = gsap.timeline()
tl.to(...)                 // 添加到时间轴末尾
tl.to(..., '<')            // 与上一个动画同时开始
tl.to(..., '-=0.5')        // 比上一个动画提前 0.5 秒
tl.to(..., '+=0.3')        // 比上一个动画延后 0.3 秒

// ── 控制方法 ──
tl.play()                  // 播放
tl.pause()                 // 暂停
tl.reverse()               // 反向播放
tl.restart()               // 重新开始
tl.progress(0.5)           // 跳到 50% 位置

// ── 常用属性 ──
{
  x: 100,          // translateX（像素）
  y: -50,          // translateY（像素）
  rotation: 360,   // 旋转（度）
  scale: 1.5,      // 缩放
  opacity: 0,      // 透明度
  duration: 1,     // 持续时间（秒）
  delay: 0.5,      // 延迟（秒）
  stagger: 0.1,    // 多元素间隔时间
  ease: 'power2.out',
  onComplete: () => { console.log('完成') }
}
```

---

## 🧊 Three.js 使用文档

### 什么是 Three.js？

**Three.js** 是一个基于 WebGL 的 3D 渲染库，可以在浏览器中创建和显示 3D 图形。
本项目用它来渲染 Kina SaQina 的 3D 角色模型。

### 安装状态

```json
// package.json 中已安装
"three": "latest",
"@types/three": "latest"
```

### 基础用法 — 在 Vue 3 中使用 Three.js

#### 1. 基本场景搭建

```typescript
import { onMounted, onUnmounted, ref } from 'vue'
import * as THREE from 'three'

const containerRef = ref<HTMLDivElement>()

let scene: THREE.Scene
let camera: THREE.PerspectiveCamera
let renderer: THREE.WebGLRenderer
let animationId: number

onMounted(() => {
  if (!containerRef.value) return

  const width = containerRef.value.clientWidth
  const height = containerRef.value.clientHeight

  // 1. 创建场景
  scene = new THREE.Scene()
  scene.background = null  // 透明背景

  // 2. 创建相机
  camera = new THREE.PerspectiveCamera(45, width / height, 0.1, 1000)
  camera.position.set(0, 1, 3)
  camera.lookAt(0, 0.5, 0)

  // 3. 创建渲染器
  renderer = new THREE.WebGLRenderer({
    antialias: true,
    alpha: true  // 透明背景
  })
  renderer.setSize(width, height)
  renderer.setPixelRatio(window.devicePixelRatio)
  renderer.shadowMap.enabled = true
  containerRef.value.appendChild(renderer.domElement)

  // 4. 添加光源
  const ambientLight = new THREE.AmbientLight(0xffffff, 0.6)
  scene.add(ambientLight)

  const directionalLight = new THREE.DirectionalLight(0xffffff, 0.8)
  directionalLight.position.set(5, 10, 5)
  directionalLight.castShadow = true
  scene.add(directionalLight)

  // 5. 动画循环
  function animate() {
    animationId = requestAnimationFrame(animate)
    renderer.render(scene, camera)
  }
  animate()
})

// 清理资源
onUnmounted(() => {
  cancelAnimationFrame(animationId)
  renderer?.dispose()
})
```

#### 2. 加载 GLTF/GLB 3D 模型

```typescript
import { GLTFLoader } from 'three/addons/loaders/GLTFLoader.js'
import { OrbitControls } from 'three/addons/controls/OrbitControls.js'

onMounted(() => {
  // ... 场景搭建代码 ...

  // 加载 3D 模型
  const loader = new GLTFLoader()
  loader.load(
    '/models/kina-saqina.glb',  // 模型文件路径
    (gltf) => {
      const model = gltf.scene
      model.scale.set(1, 1, 1)
      model.position.set(0, 0, 0)

      // 启用阴影
      model.traverse((child) => {
        if ((child as THREE.Mesh).isMesh) {
          child.castShadow = true
          child.receiveShadow = true
        }
      })

      scene.add(model)

      // 播放模型动画（如有）
      if (gltf.animations.length > 0) {
        const mixer = new THREE.AnimationMixer(model)
        const action = mixer.clipAction(gltf.animations[0])
        action.play()

        // 在动画循环中更新
        const clock = new THREE.Clock()
        function animateWithMixer() {
          requestAnimationFrame(animateWithMixer)
          mixer.update(clock.getDelta())
          renderer.render(scene, camera)
        }
        animateWithMixer()
      }
    },
    (progress) => {
      // 加载进度
      const percent = (progress.loaded / progress.total) * 100
      console.log(`模型加载中: ${percent.toFixed(1)}%`)
    },
    (error) => {
      console.error('模型加载失败:', error)
    }
  )

  // 轨道控制器（鼠标交互）
  const controls = new OrbitControls(camera, renderer.domElement)
  controls.enableDamping = true
  controls.dampingFactor = 0.05
  controls.enableZoom = false  // 禁用缩放
  controls.autoRotate = true   // 自动旋转
  controls.autoRotateSpeed = 1.5
})
```

#### 3. 在 Vue 模板中使用

```vue
<template>
  <div class="profile__right">
    <div ref="containerRef" class="model-container"></div>
    <button class="btn-3d" @click="toggle3D">
      <span>3D</span>
    </button>
  </div>
</template>

<style lang="scss" scoped>
.model-container {
  width: 100%;
  height: 100%;
  min-height: 400px;

  canvas {
    display: block;
    width: 100% !important;
    height: 100% !important;
  }
}
</style>
```

#### 4. 本项目推荐的 Three.js 集成方案

```typescript
// 在 BerryChanPage.vue 的 <script setup> 中
import { onMounted, onUnmounted, ref } from 'vue'
import * as THREE from 'three'
import { GLTFLoader } from 'three/addons/loaders/GLTFLoader.js'
import { OrbitControls } from 'three/addons/controls/OrbitControls.js'
import gsap from 'gsap'  // 结合 GSAP 做入场动画

const modelContainer = ref<HTMLDivElement>()
let renderer: THREE.WebGLRenderer
let animationId: number

function initThreeJS() {
  if (!modelContainer.value) return

  const w = modelContainer.value.clientWidth
  const h = modelContainer.value.clientHeight

  // 场景
  const scene = new THREE.Scene()

  // 相机
  const camera = new THREE.PerspectiveCamera(40, w / h, 0.1, 100)
  camera.position.set(0, 1.2, 3.5)

  // 渲染器（透明背景，与页面融合）
  renderer = new THREE.WebGLRenderer({ antialias: true, alpha: true })
  renderer.setSize(w, h)
  renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2))
  renderer.outputColorSpace = THREE.SRGBColorSpace
  renderer.toneMapping = THREE.ACESFilmicToneMapping
  renderer.toneMappingExposure = 1.2
  modelContainer.value.appendChild(renderer.domElement)

  // 光源
  scene.add(new THREE.AmbientLight(0xffffff, 0.5))
  const keyLight = new THREE.DirectionalLight(0xffffff, 1)
  keyLight.position.set(3, 5, 4)
  scene.add(keyLight)
  const rimLight = new THREE.DirectionalLight(0xffd600, 0.3)
  rimLight.position.set(-3, 3, -2)
  scene.add(rimLight)

  // 轨道控制
  const controls = new OrbitControls(camera, renderer.domElement)
  controls.enableDamping = true
  controls.enableZoom = false
  controls.minPolarAngle = Math.PI / 3
  controls.maxPolarAngle = Math.PI / 2
  controls.autoRotate = true
  controls.autoRotateSpeed = 1

  // 加载模型
  const loader = new GLTFLoader()
  loader.load('/models/kina-saqina.glb', (gltf) => {
    const model = gltf.scene
    scene.add(model)

    // GSAP 入场动画
    gsap.from(model.position, { y: -2, duration: 1.5, ease: 'power3.out' })
    gsap.from(model.rotation, { y: Math.PI, duration: 1.5, ease: 'power2.out' })
  })

  // 动画循环
  function animate() {
    animationId = requestAnimationFrame(animate)
    controls.update()
    renderer.render(scene, camera)
  }
  animate()

  // 响应窗口变化
  window.addEventListener('resize', () => {
    if (!modelContainer.value) return
    const nw = modelContainer.value.clientWidth
    const nh = modelContainer.value.clientHeight
    camera.aspect = nw / nh
    camera.updateProjectionMatrix()
    renderer.setSize(nw, nh)
  })
}

onMounted(() => initThreeJS())
onUnmounted(() => {
  cancelAnimationFrame(animationId)
  renderer?.dispose()
})
```

### Three.js 常用概念速查

| 概念 | 说明 | 类名 |
|------|------|------|
| **场景** | 3D 世界的容器 | `THREE.Scene` |
| **相机** | 观察 3D 世界的视角 | `THREE.PerspectiveCamera` |
| **渲染器** | 将 3D 场景画到屏幕上 | `THREE.WebGLRenderer` |
| **几何体** | 3D 物体的形状 | `THREE.BoxGeometry` 等 |
| **材质** | 物体的外观/纹理 | `THREE.MeshStandardMaterial` |
| **网格** | 几何体 + 材质 = 可见物体 | `THREE.Mesh` |
| **光源** | 照亮场景的光 | `THREE.DirectionalLight` 等 |
| **加载器** | 加载外部 3D 模型 | `GLTFLoader` |
| **控制器** | 鼠标/触摸交互 | `OrbitControls` |

### Three.js 性能优化建议

```typescript
// 1. 限制像素比（移动端性能优化）
renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2))

// 2. 模型优化 — 减少面数
// 使用 Blender 的 Decimate 修改器

// 3. 纹理压缩
// 使用 KTX2 格式 + KTX2Loader

// 4. 按需渲染（不需要持续动画时）
let needsUpdate = true
controls.addEventListener('change', () => { needsUpdate = true })
function animate() {
  requestAnimationFrame(animate)
  if (needsUpdate) {
    renderer.render(scene, camera)
    needsUpdate = false
  }
}

// 5. 内存清理
function dispose() {
  scene.traverse((object) => {
    if (object instanceof THREE.Mesh) {
      object.geometry.dispose()
      if (Array.isArray(object.material)) {
        object.material.forEach(m => m.dispose())
      } else {
        object.material.dispose()
      }
    }
  })
  renderer.dispose()
}
```

---

## 🎨 设计系统

### SCSS 变量（设计令牌）

```scss
// 文件: src/style.scss

// 颜色
$yellow:      #FFD600;   // 主色调 — 黄色
$dark:        #1a1a1a;   // 深色背景/文字
$white:       #FFFFFF;   // 白色
$teal:        #00CED1;   // 青色强调线
$accent-red:  #E8456B;   // 红色强调
$gray-mid:    #888888;   // 中灰色
$tag-bg:      #2a2a2a;   // 标签值背景

// 字体
$font-en: 'Outfit', 'Inter', system-ui, sans-serif;
$font-cn: 'Noto Sans SC', sans-serif;
```

### 水印文字 — 斜线纹理（arsir/hatching）效果

```scss
.hero__watermark {
  // 使用 repeating-linear-gradient 创建斜线填充
  background: repeating-linear-gradient(
    -45deg,
    rgba(0, 0, 0, 0.18) 0px,
    rgba(0, 0, 0, 0.18) 2.5px,
    rgba(0, 0, 0, 0.04) 2.5px,
    rgba(0, 0, 0, 0.04) 6px
  );
  -webkit-background-clip: text;
  background-clip: text;
  color: transparent;
}
```

---

## 📌 后续开发计划

- [ ] 集成 GSAP 页面入场动画
- [ ] 集成 Three.js 3D 模型渲染
- [ ] 添加 3D 模型文件（GLB/GLTF 格式）
- [ ] 实现 3D 按钮切换功能
- [ ] 添加滚动触发动画（GSAP ScrollTrigger）
- [ ] 移动端响应式优化
- [ ] 添加页面过渡动画
- [ ] 性能优化与 Lighthouse 审计

---

## 📄 许可证

MIT License

---

> **注意**: 本文档为 AI 辅助开发文档，旨在帮助其他 AI 模型或开发者无缝接续本项目的开发工作。
> 所有代码示例均可直接在本项目中使用。
