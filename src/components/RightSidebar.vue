<template>
<div>
  <!--Loads right sidebar-->
<div class='scroll-hidden'>
    <div class='bg-darken10 viewport-twothirds viewport-full-ml absolute top right bottom'></div>
    <div class='absolute top-ml right bottom z1 w-full w600-ml px12 py12-ml'>
        <!-- abas -->
        <slot name="tabs"></slot>
        <!-- conteudo -->
        <div id="content" class=' initial-size flex-parent flex-parent--column viewport-half h-auto-ml hmax-full bg-white shadow-darken10'>
          <slot name="content"></slot>
        </div>
    </div>
</div>
</div>
</template>
