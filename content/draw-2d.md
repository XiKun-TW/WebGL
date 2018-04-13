<section>
    <h3> Hello World ！ WebGL </h3>
    <ol style="font-size: 70%">
        <li>画一个点</li>
        <li>画五个点</li>
        <li>画线</li>
        <li>画三角形</li>
    </ol>
</section>

<section>
    <p>先来个暖场show case</p>
    <img src="/img/show case.gif" width="400" height="400"></img>
</section>

<section>
    <p>画一个点需要几步？</p>
    <ol style="font-size:70%">
        <li>建好画舫 (create canvas)</li>
        <li>选好画风 (get context) </li>
        <li>造画笔 (init Vertex Shader)</li>
        <li>造调色板 (init Fragment Shader)</li>
        <li>将造好的画笔、调色板分配给画舫 (use program)</li>
        <li>在画布上描一个点 (pass one value to Vertex Shader)</li>
        <li>给点上色 (pass value to Fragment Shader)</li>
    </ol>
</section>

<section>
    <p>建画舫</p>
    <pre>
        <code data-trim data-noescape>
        ```
<body>
    ...
    <canvas id='canvas' width="500" height="500"></canvas>
    ...
</body>
        ```
        </code>
    </pre>
</section>

<section>
    <p>选画风</p>
    <pre>
        <code class="js">
//javascript
function main() {
    const canvasElement = document.getElementById('canvas');
    const context = canvasElement.getContext('webgl');
}
        </code>
    </pre>
</section>

<section>
    <p>造画笔 (init Vertex Shader)</p>
    <pre>
        <code data-trim data-noescape>
        ```
<body>
    ...
    <script id="vertex-shader" type="notjs">
        attribute vec4 a_position;
        attribute float a_pointsize;
        
        void main() {
            gl_Position = a_position;
            gl_PointSize = a_pointsize;
        }
    </script>
    ...
</body>
        ```
        </code>
    </pre>
</section>

<section>
    <p>造画笔 (init Vertex Shader)</p>
    <pre>
        <code class="js">
//创建 shader 的方法
function createShader(gl, shaderType, shaderScript) {
    const shader = gl.createShader(shaderType);
    gl.shaderSource(shader, shaderScript);
    gl.compileShader(shader);
    const success = 
        gl.getShaderParameter(shader, gl.COMPILE_STATUS);
    
    if (success) {
        return shader;
    }
    console.log(gl.getShaderInfoLog(shader));
    gl.deleteShader(shader);
}
        </code>
    </pre>
</section>

<section>
    <p>造画笔 (init Vertex Shader)</p>
    <pre>
        <code class="js">
//初始化顶点 shader 的方法
function main() {
    ...
    const vertexShaderScript = 
        document.getElementById("vertex-shader").text;

    const vertextShader =
        createShader(gl, gl.VERTEX_SHADER, vertexShaderScript);
    ...
}
        </code>
    </pre>
</section>

<section>
    <p>造调色板 (init Fragment Shader)</p>
    <pre>
    <code data-trim data-noescape>
        ```
<body>
    ...
    <script id="fragment-shader" type="notjs">
    precision mediump float;
    uniform vec4 a_color;
    void main() {
        gl_FragColor = a_color;
    }
    </script>
    ...
</body>
        ```
        </code>
    </pre>
</section>

<section>
    <p>造调色板 (init Vertex Shader)</p>
    <pre>
        <code class="js">
//初始化fragment shader 的方法
function main() {
    ...
    const fragmentShaderScript= 
        document.getElementById("fragment-shader").text;

    const fragmentShader = 
        createShader(gl, gl.FRAGMENT_SHADER, 
            fragmentShaderScript);
    ...
}
        </code>
    </pre>
</section>

<section>
    <p>将造好的画笔、调色板分配给画舫 (use program)</p>
    <pre>
        <code class="js">
//创建着色器方法
function createProgram(gl, vertexShader, fragmentShader) {
    var program = gl.createProgram();
    gl.attachShader(program, vertexShader);
    gl.attachShader(program, fragmentShader);
    gl.linkProgram(program);
    var success = 
        gl.getProgramParameter(program, gl.LINK_STATUS);
        
    if (success) {
        return program;
    }
    console.log(gl.getProgramInfoLog(program));
    gl.deleteProgram(program);
}
        </code>
    </pre>
</section>

<section>
    <p>将造好的画笔、调色板分配给画舫 (use program)</p>
    <pre>
        <code class="js">
function main() {
    ...
    const program = 
        createProgram(gl, vertexShader, fragmentShader);
    gl.useProgram(program);
    ...
}
        </code>
    </pre>
</section>

<section>
    <p>在画布上描一个点 (pass one value to Vertex Shader)</p>
    <pre>
        <code class="js">
function main() {
    ...
    const a_position = 
        gl.getAttribLocation(program, 'a_position');
    const a_pointsize = 
        gl.getAttribLocation(program, 'a_pointsize');

    gl.vertexAttrib3f(a_position, 0.0, 0.0, 0.0);
    gl.vertexAttrib1f(a_pointsize, 10.0);
    ...
}
        </code>
    </pre>
</section>

<section>
    <p>上色 (pass one value to Fragment Shader)</p>
    <pre>
        <code class="js">
function main() {
    ...
    const a_color = 
        gl.getUniformLocation(program, 'a_color');
    gl.uniform4f(a_color, 1.0, 0.0, 0.0,1.0);

    gl.clearColor(0, 0, 0, 1);
    gl.clear(gl.COLOR_BUFFER_BIT);

    gl.drawArrays(gl.POINTS, 0, 1);
    ...
}
        </code>
    </pre>
</section>

<section>
    <p>dang lang lang ~</p>
    <img src="/img/one point.png" width="400" height="400"></img>
</section>

<section>
    <p>信心大增，怒画五个点</p>
    <pre>
        <code class="js">
function main() {
    ...
    gl.vertexAttrib3f(a_position, 0.5, 0.5, 0.0);
    gl.vertexAttrib1f(a_pointsize, 10.0);
    gl.uniform4f(a_color, 0.0, 1.0, 0.0 ,1.0);
    gl.drawArrays(gl.POINTS, 0, 1);

    gl.vertexAttrib3f(a_position, 0.5, -0.5, 0.0);
    gl.vertexAttrib1f(a_pointsize, 10.0);
    gl.uniform4f(a_color, 1.0, 1.0, 0.0 ,1.0);
    gl.drawArrays(gl.POINTS, 0, 1);
    ...
}
        </code>
    </pre>
</section>

<section>
    <p>so easy ~</p>
    <img src="/img/five points.png" width="400" height="400"></img>
</section>

<section>
    <p>画线需要几步？</p>
    <ol style="font-size:70%">
        <li>建好画舫 (create canvas)</li>
        <li>选好画风 (get context) </li>
        <li>造画笔 (init Vertex Shader)</li>
        <li>造调色板 (init Fragment Shader)</li>
        <li>将造好的画笔、调色板分配给画舫 (use program)</li>
        <li class="fragment highlight-red">造样片 (create buffer)</li>
        <li class="fragment highlight-red">分别在画布上描两个点 (pass value list to Vertex Shader)</li>
        <li class="fragment highlight-red">将两点连线并上色 (pass value list to Fragment Shader)</li>
    </ol>
</section>

<section>
    <p>造样片 (create buffer)</p>
    <pre>
        <code data-trim data-noescape>
```
<body>
    ...
    <script id="vertex-shader" type="notjs">
        attribute vec4 a_position;
        attribute vec4 a_color;
        varying vec4 v_color;
        void main() {
            gl_Position = a_position;
            v_color = a_color;
        }
    </script>
    <script id="fragment-shader" type="notjs">
        precision mediump float;
        varying vec4 v_color;
        void main() {
            gl_FragColor = v_color;
        }
    </script>
    ...
</body>
```
        </code>
    </pre>
</section>

<section>
    <p>造样片 (create buffer)</p>
    <pre>
        <code class="js">
function initVertexBuffers(gl, program) {
    const vertices = new Float32Array([
        0.0, 0.0, 1.0, 0.0, 0.0,
        0.5, 0.5, 0.0, 1.0, 0.0,
        0.5, -0.5, 0.0, 0.0, 1.0,
        -0.5, -0.5, 1.0, 1.0, 0.0,
        -0.5, 0.5, 0.0, 1.0, 1.0,
    ]);

    var n = 5;

    const FSIZE = vertices.BYTES_PER_ELEMENT;
  
    const vertexBuffer = gl.createBuffer();
    gl.bindBuffer(gl.ARRAY_BUFFER, vertexBuffer);
    gl.bufferData(gl.ARRAY_BUFFER, vertices, gl.STATIC_DRAW);

    const a_position = 
        gl.getAttribLocation(program, 'a_position');
    const v_color = 
        gl.getAttribLocation(program, 'a_color');

    gl.vertexAttribPointer(a_position, 2, gl.FLOAT, 
        false, FSIZE x 5, 0);
    gl.vertexAttribPointer(v_color, 3, gl.FLOAT, 
        false, FSIZE x 5, FSIZE x 2);

    gl.enableVertexAttribArray(a_position);
    gl.enableVertexAttribArray(v_color);
    return n;
}
        </code>
    </pre>
</section>

<section>
    <p>描点并上色</p>
    <pre>
        <code class="js">
function main() {
    ...
    const n = initVertexBuffers(gl, program);
  
    gl.drawArrays(gl.LINES, 0, n);
    //gl.drawArrays(gl.LINE_STRIP, 0, n);
    //gl.drawArrays(gl.LINE_LOOP, 0, n);
    ...
}
        </code>
    </pre>
</section>

<section>
    <p>draw lines (gl.LINES)</p>
    <img src="/img/draw lines.png" width="400" height="400"></img>
</section>

<section>
    <p>draw lines strip (gl.LINE_STRIP)</p>
    <img src="/img/draw line strip.png" width="400" height="400"></img>
</section>

<section>
    <p>draw line loop (gl.LINE_LOOP)</p>
    <img src="/img/draw line loop.png" width="400" height="400"></img>
</section>

<section>
    <p>画三角形需要几步？</p>
</section>

<section>
    <p>描点并上色</p>
    <pre>
        <code class="js">
function main() {
    ...
    const n = initVertexBuffers(gl, program);
  
    gl.drawArrays(gl.TRIANGLES, 0, n);
    //gl.drawArrays(gl.TRIANGLE_STRIP, 0, n);
    //gl.drawArrays(gl.TRIANGLE_FAN, 0, n);
    ...
}
        </code>
    </pre>
</section>

<section>
    <p>draw triangles (gl.TRIANGLES)</p>
    <img src="/img/draw triangles.png" width="400" height="400"></img>
</section>

<section>
    <p>draw triangle strip (gl.TRIANGLE_STRIP)</p>
    <img src="/img/draw triangle strip.png" width="400" height="400"></img>
</section>

<section>
    <p>draw triangle fan (gl.TRIANGLE_FAN)</p>
    <img src="/img/draw triangle fan.png" width="400" height="400"></img>
</section>