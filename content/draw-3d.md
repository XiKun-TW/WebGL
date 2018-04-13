<section>
    <h3> WebGL for 3D! </h3>
    <ol style="font-size: 70%">
        <li>what is 3D ?</li>
        <li>怎么描述一个 3D 场景？</li>
        <li>画一个3D立方体</li>
    </ol>
</section>

<section>
    <p>什么是 3D?</p>
    <ol style="font-size: 70%">
        <li class="fragment">数据使用三维坐标系统表示</li>
        <li class="fragment">最终被绘制为一个2D图像</li>
        <li class="fragment">它支持实时显示，即数据发生变化时能基本无延迟更新图像</li>
    </ol>
</section>

<section>
    <p>怎么描述一个3D场景？</p>
    <ol style="font-size: 70%">
        <li>视点视线</li>
        <li>可视范围</li>
    </ol>
</section>

<section>
    <p>视点视线</p>
    <ol style="font-size: 70%">
        <li>视点</li>
        <li>观察目标点</li>
        <li>上方向</li>
    </ol>
</section>

<section>
    <p>视点视线</p>
    <img src="/img/sight.png" width="400" height="400"></img>
</section>

<section>
    <p>可视范围</p>
    <ol style="font-size: 70%">
        <li>盒状可视投影</li>
        <li>透视投影</li>
    </ol>
</section>

<section>
    <p>盒装可视投影</p>
    <img src="/img/box shadow.png" width="500" height="400"></img>
</section>

<section>
    <p>透视投影</p>
    <img src="/img/sight shadow.png" width="500" height="400"></img>
</section>

<section>
    <p>在webgl里面怎么表示呢？</p>
</section>

<section>
    <p>通过矩阵变换！</p>
    <img src="/img/matrix.png" width="400" height="400"></img>
</section>

<section>
    <p>画一个3D立方体需要几步？</p>
    <ol style="font-size: 70%">
        <li>....</li>
        <li class="fragment highlight-red">改样片(change buffer data)</li>
        <li class="fragment highlight-red">设定视角</li>
        <li>....</li>
    </ol>
</section>

<section>
    <p>改样片(change buffer data)</p>
    <img width="500" height="500" src="/img/cube coord.png"></img>
</section>

<section>
    <p>改样片(change buffer data)</p>
    <pre>
        <code class="js">
// Create a cube
//    v6----- v5
//   /|      /|
//  v1------v0|
//  | |     | |
//  | |v7---|-|v4
//  |/      |/
//  v2------v3
// 第一面：V0 = 1.0, 1.0, 1.0, 1.0, 1.0, 0.0 
// 前三个数字是坐标，后三个数字是颜色
// 简写如下
const vertices = new Float32Array([
    V0, V1, V2, V0, V2, V3, //第一个面
    V4  V0, V3, V4, V5, V0  //第二个面
    V5, V6, V7, V5, V7, V4, //第三个面
    V6, V2, V7, V6, V1, V2, //第四个面
    V4, V7, V2, V4, V2, V3, //第五个面
    V5, V0, V3, V5, V3, V4, //第六个面
]);
        </code>
    </pre>
</section>

<section>
    <p>设定视角</p>
    <pre>
        <code data-trim data-noescape>
```
<body>
    ...
    <script id="vertex-shader" type="notjs">
        attribute vec4 a_position;
        attribute vec4 a_color;
        uniform mat4 u_viewmatrix;
        varying vec4 v_color;
        void main() {
            gl_Position = u_viewmatrix * a_position;
            v_color = a_color;
        }
    </script>
    ...
</body>
```
        </code>
    </pre>
</section>

<section>
    <p>duang~ duang~ duang~</p>
    <img src="/img/cube.png" width="400" height="400"></img>
</section>