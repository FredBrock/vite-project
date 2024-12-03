<script>
  import { createPopper } from "@popperjs/core";
  import { onMount, tick } from "svelte";

  let _timer;
  let showDelay = 200;
  let popperInstance;
  let popperStatus = false;
  let referenceEl;
  let popperEl;

  $: showDisplay = popperStatus ? "block" : "none";
  function showPopper() {
    console.log("showPopper");
    clearTimeout(_timer);
    _timer = setTimeout(() => {
      popperStatus = true;

      tick().then(() => {
        if (popperInstance) {
          console.log("popperInstance.update()");
          popperInstance.update();
        //   popperInstance.forceUpdate();
        }
      });
    }, showDelay);
  }

  function hidePopper() {
    clearTimeout(_timer);
    _timer = setTimeout(() => {
      popperStatus = false;
    }, showDelay);
  }

  function toggle(e) {
    e.stopPropagation();
    e.preventDefault();
    popperStatus = !popperStatus;
  }

  function updatePopper(params) {
    if (popperInstance) {
      popperInstance.update();
    }
  }
  function handleResize() {
    if (popperInstance) {
      popperInstance.update();
    }
  }

  function destroyPopper() {
    if (popperInstance) {
      popperInstance.destroy();
      popperInstance = null;
    }
  }
  function onPopperMouseover() {
    clearTimeout(_timer);
  }
  function onPopperMouseout() {
    _timer = setTimeout(() => {
      popperStatus = false;
    }, showDelay);
  }
  function onPopperClick(e) {
    e.stopPropagation();
  }
  function onPopperKeydown(e) {
    if (e.key === "Escape") {
      popperStatus = false;
    }
  }

  function init(node) {
    // const referenceElement = document.querySelector("button");
    // const popperElement = document.querySelector(".popover");
    const arrowElement = document.querySelector(".popper-arrow");
    console.log(node);
    const referenceElement = node;
    const popperElement = node.nextElementSibling;
    console.log(popperElement);
    popperInstance = createPopper(referenceElement, popperElement, {
      placement: "left",
      modifiers: [
        {
          name: "eventListeners",
          enabled: true,
        },
        {
          name: "offset",
          options: {
            offset: [0, 24],
          },
        },
        {
          name: "preventOverflow",
          options: {
            boundary: "window", // 同样设置边界为窗口
            // altAxis: false, 
            // mainAxis: true, 
            // padding: 800,
            // rootBoundary: 'document',
          },
        },
        {
          name: "flip",
          enabled: false, // 禁用 flip，防止自动修改位置
        },
        {
          name: "arrow",
          options: {
            element: arrowElement,
          },
        },
      ],
    });
    window.addEventListener("resize", handleResize);
    return () => {
      destroyPopper();
      window.removeEventListener("resize", handleResize);
    };
  }

  onMount(() => {
    // const referenceElement = document.querySelector("button");
    // const popperElement = document.querySelector(".popover");
    // const arrowElement = document.querySelector(".popper-arrow");
    // // console.log(referenceElement, popperElement);
    // popperInstance = createPopper(referenceElement, popperElement, {
    //   placement: "left",
    //   modifiers: [
    //     {
    //       name: "eventListeners",
    //       enabled: true,
    //     },
    //     {
    //       name: "offset",
    //       options: {
    //         offset: [0, 8],
    //       },
    //     },
    //     {
    //       name: "arrow",
    //       options: {
    //         element: arrowElement,
    //       },
    //     },
    //     {
    //       name: "flip",
    //       options: {
    //         fallbackPlacements: ["top", "bottom"],
    //       },
    //     },
    //   ],
    // });
    // window.addEventListener("resize", handleResize);
    return () => {
      destroyPopper();
      window.removeEventListener("resize", handleResize);
    };
  });
</script>

<button
  on:mouseover={showPopper}
  on:mouseout={hidePopper}
  use:init
  bind:this={referenceEl}
>
  <slot name="trigger"></slot>
</button>

<div
  class="popover"
  style:display={showDisplay}
  bind:this={popperEl}
  on:mouseover={onPopperMouseover}
  on:mouseout={onPopperMouseout}
>
  <div class="popover-content">
    <slot name="content"></slot>
  </div>
  <div class="popper-arrow"></div>
</div>
