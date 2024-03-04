<script>
    import "../../app.css";
    import { onMount } from 'svelte';
    let temp = 0;
    let angle = 0;

    onMount(() => {
        const canvas = document.getElementById("myCanvas");
        if (!(canvas instanceof HTMLCanvasElement)) {
            throw new Error("Element is not a canvas");
        }
        const ctx = canvas.getContext("2d");

        canvas.addEventListener('mousedown', function(e) {
            canvas.addEventListener('mousemove', onMouseMove, false);
        }, false);

        canvas.addEventListener('mouseup', function() {
            canvas.removeEventListener('mousemove', onMouseMove, false);
        }, false);

        /**
         * @param {MouseEvent} e
         */
        function onMouseMove(e) {
            if (!(canvas instanceof HTMLCanvasElement)) {
                throw new Error("Element is not a canvas");
            }

            var rect = canvas.getBoundingClientRect();
            var x = e.clientX - rect.left - canvas.width / 2;
            var y = e.clientY - rect.top - canvas.height / 2;
            var newAngle = Math.atan2(y, x);
            var delta = newAngle - angle;
            angle = newAngle;
            temp += delta * 50; // Change this to adjust sensitivity
            temp = Math.max(Math.min(temp, 240), 0); // Clamp between 0 and 240
            draw();
        }

        function draw() {
            if (!(canvas instanceof HTMLCanvasElement) || !ctx) {
                throw new Error("Element is not a canvas");
            }

            ctx.clearRect(0, 0, canvas.width, canvas.height);
            ctx.beginPath();
            ctx.moveTo(canvas.width / 2, canvas.height / 2);
            ctx.lineTo(canvas.width / 2 + 200 * Math.cos(angle), canvas.height / 2 + 200 * Math.sin(angle));
            ctx.stroke();
            ctx.font = "30px Arial";
        }

        draw();
    });
</script>



<div class="bg-slate-300 flex flex-col items-center w-min">
    <div class="px-20 py-4 flex items-center">
        <div class="rounded-full overflow-hidden border-2 border-black">
        <canvas id="myCanvas" width="30" height="30" class="">
            Your browser does not support the HTML5 canvas tag.
        </canvas>
        </div>
        <div class="bg-black text-white w-24 p-1 mx-4">
            <p>{Math.round(temp)} °C</p>
        </div>
        
    </div>
    <div class="flex flex-col items-center border-t-4 border-b-4 border-black w-full">
        <div class="px-28 py-1 bg-slate-400 mb-4 mt-2 rounded-lg"></div>
        <div class="bg-black p-4 rounded-md mb-2">
            <div class="bg-gray-800 px-20 py-12"></div>
        </div>
        <p class="text-sm text-gray-200 mb-4">Ovn</p>
    </div>
</div> 
