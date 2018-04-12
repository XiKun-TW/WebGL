<section>
    <h3> 蹦进 WebGL 的大门 </h3>
    <ol>
        <li>WebGL网页的结构</li>
        <li>canvas标签</li>
        <li>着色器语言 (shading language)</li>
    </ol>
</section>

<section>
<small>在普通的 Web 网页中应该包含两种语言： HTML 和 Javascript（CSS）, 而引入 WebGL 后还需要加入着色器语言 GLSL ES。如下图所示：</small>
<img class="fragment" src="/img/web vs webGl.png"></img>
</section>

<section>
    <p>canvas 标签</p>
    <small>canvas 标签是 HTML5 定义的一个新的 DOM 元素，它将页面中的一个区域定义为可绘制区域。而canvas 元素仅仅声明了页面中的某个区域来进行绘画。在绘画的时候，我们需要通过<span class="fragment highlight-red">上下文(context)</span>对象绘制, 这个对象提供了绘图的API。</small>
</section>

<section> 
    <p>使用canvas标签获取上下文（context）</p>
    <pre>
        <code data-trim data-noescape>
        //HTML
        ```
        <body>
            ...
            <canvas id='canvas'></canvas>
            ...
        <body>
        ```
        </code>
    </pre>
    <pre>
        <code>
//javascript
const canvasElement = document.getElementById('canvas');
const context = canvasElement.getContext(contentType);
        </code>
    </pre>
</section>

<section>
    <p>contextType</p>
    <table style="font-size:60%">
        <thead>
            <tr>
                <th>
                    参数名称
                </th>
                <th>
                    参数描述
                </th>
            </tr>
        </thead>
        <tbody>
            <tr class="fragment">
                <td>
                    2d
                </td>
                <td>
                    创建一个 CanvasRenderingContext2D 对象代表一个二维渲染上下文
                </td>
            </tr>
            <tr class="fragment">
                <td>
                    webgl
                </td>
                <td>
                    创建一个 WebGLRenderingContext 代表三维渲染上下文对象。版本1 (OpenGL ES 2.0)
                </td>
            </tr>
            <tr class="fragment">
                <td>
                    webgl2
                </td>
                <td>
                    创建一个 WebGL2RenderingContext 代表三维渲染上下文对象。版本2 (OpenGL ES 3.0)。
                </td>
            </tr>
            <tr class="fragment">
                <td>
                    bitmaprenderer
                </td>
                <td>
                    创建一个 ImageBitmapRenderingContext 只提供功能去替换指定 canvas 的ImageBitmap内容
                </td>
            </tr>
        </tbody>
    </table>
</section>

<section>
    <p>着色器语言</p>
    <small><strong>着色器语言</strong>是用来在OpenGL中着色编程的语言，也即开发人员写的短小的自定义程序，他们是在图形卡的GPU （Graphic Processor Unit图形处理单元）上执行的，其语法和用法和 C 语言极为相似。用该语言编写的用于实现精美视觉效果的程序称之为着色器。着色器又分为：<span class="fragment highlight-red">顶点着色器 (Vertex Shader) </span> 和 <span class="fragment highlight-red">片元着色器(Fragment Shader)。</span></small>
</section>

<section>
    <p>来，总结下我们接触的新名词</p>
    <ol>
        <li class="fragment">OpenGL</li>
        <li class="fragment">OpenGL ES</li>
        <li class="fragment">canvas</li>
        <li class="fragment">canvas context type</li>
        <li class="fragment">GLSL ES</li>
        <li class="fragment">顶点着色器 (Vertex Shader)</li>
        <li class="fragment">片元着色器 (Fragment Shader)</li>
    </ol>
</section>

<section>
    <p class="fragment">这么多新名词！怎么蹦？</p>
    <img width="400px" height="400px" src="/img/question.png"></img> 
</section>

<section>
    <p>从现在起把自己当作画家！</p>
    <ul>
        <li class="fragment">canvas ->  画舫（画布、绘画技能) </li>
        <li class="fragment">canvas context type -> 画风 </li>
        <li class="fragment">顶点着色器（Vertex Shader） -> 描点</li>
        <li class="fragment">片元着色器（Fragment Shader） -> 上色</li>
    </ul>
</section>
