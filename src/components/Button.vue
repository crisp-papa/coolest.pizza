<template>
  <div class="container">
    <div class="button" v-on:click="$emit('button-click')">
      <span>{{ title }}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Button',
  data: function() { 
    return { 

    }
  },
  props: {
    title: String,
    backgroundColor: String,
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="less">
  .container { 
    min-width: 100%;
    padding: 0 4px;
    display: inline-block;

    @media (min-width: 768px) { 
      min-width: 50%;
    }

    @media (min-width: 1024px) { 
      min-width: 25%;
    }
  }
  .button { 
    user-select: none;
    position: relative;
    background-color: rgb(67, 131, 173);
    font-size: 1.5em;
    height: 75px;
    width: 100%;
    text-align: center;
    line-height: 75px;
    box-shadow: 4px 4px 0 0 rgba(0,0,0,0.75);
    margin-right: 4px;
    margin-bottom: 4px;
    cursor: pointer;

    &:hover { 
      box-shadow: 2px 2px 0 0 rgba(0,0,0,0.75);
      top: 2px;
      left: 2px;
    }

    &:active { 
      box-shadow: none;
      top: 4px;
      left: 4px;
    }
  }
</style>
