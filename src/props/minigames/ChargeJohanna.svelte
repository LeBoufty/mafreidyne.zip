<script context="module">
  export const ssr = true;
</script>

<script lang="ts">
  import { onMount } from "svelte";

  let canvas: HTMLCanvasElement | null = null;
  let ctx: CanvasRenderingContext2D | null = null;
  let isDragging: boolean = false;

  const canvaswidth = 900;
  const canvasheight = 900;

  let charger = { x: 50, y: 50, width: 50, height: 50 };
  let johanna = { x: 200, y: 200, width: 100, height: 100 };

  function draw(): void {
    if (!ctx || !canvas) return;

    ctx.clearRect(0, 0, canvas.width, canvas.height);

    // Draw the draggable charger
    ctx.fillStyle = "blue";
    ctx.fillRect(charger.x, charger.y, charger.width, charger.height);

    // Draw a static charger
    ctx.fillStyle = "red";
    ctx.fillRect(johanna.x, johanna.y, johanna.width, johanna.height);
  }

  function isInsidecharger(x: number, y: number): boolean {
    return (
      x > charger.x &&
      x < charger.x + charger.width &&
      y > charger.y &&
      y < charger.y + charger.height
    );
  }

  function handleMouseDown(event: MouseEvent): void {
    if (!canvas) return;

    const rect = canvas.getBoundingClientRect();
    const x = event.clientX - rect.left;
    const y = event.clientY - rect.top;

    if (isInsidecharger(x, y)) {
      isDragging = true;
    }
  }

  function handleMouseMove(event: MouseEvent): void {
    if (!isDragging || !canvas) return;

    const rect = canvas.getBoundingClientRect();
    charger.x = event.clientX - rect.left - charger.width / 2;
    charger.y = event.clientY - rect.top - charger.height / 2;
    draw();
  }

  function handleMouseUp(): void {
    isDragging = false;
  }

  onMount(() => {
    charger.x =
      canvaswidth / 2 +
      Math.floor(Math.random() * (canvaswidth / 2 - 100) + 50);
    charger.y =
      canvaswidth / 2 +
      Math.floor(Math.random() * (canvasheight / 2 - 50) + 26);

    johanna.x = canvaswidth - 100 - charger.x;
    johanna.y = canvasheight - 100 - charger.y;

    if (!canvas) return;

    ctx = canvas.getContext("2d");
    if (ctx) {
      draw();
    }
  });
</script>

<canvas
  bind:this={canvas}
  width={canvaswidth}
  height={canvasheight}
  on:mousedown={handleMouseDown}
  on:mousemove={handleMouseMove}
  on:mouseup={handleMouseUp}
  class="bg-cyan-950 align-middle"
></canvas>
