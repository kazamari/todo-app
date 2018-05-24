<template>
  <div>
    <header>
      <div class="ui container center aligned">
        <h1>Vue.js Todo App</h1>
      </div>
    </header>
    <div class="ui main text container">
      <todo-list></todo-list>
    </div>
    <footer class="info">
      <p>Double-click to edit a todo</p>
    </footer>
  </div>
</template>

<script>
  import TodoList from './components/TodoList'

  export default {
    components: {
      TodoList
    }
  }
</script>

<style>
  body{background:#efefef;}
  header .ui.container{padding:20px 0;}
  header h1{font-size:60px;text-transform:uppercase;color:#ccc;}
  header.inverted{background:#333;}
  header.inverted h1{color:#fff;}
  .ui.main.text.container{padding:0;}
  .info{
    margin-top: 35px;
    color: #bfbfbf;
    font-size: 12px;
    text-shadow: 0 1px 0 rgba(255, 255, 255, 0.5);
    text-align: center;
  }
  .new-todo{border:0 none;padding:0 0 0 45px;width:100%;font-size:18px;height:24px;}
  ::-webkit-input-placeholder { /* Chrome */
    font-style:italic;
    color: #eee;
  }
  :-ms-input-placeholder { /* IE 10+ */
    font-style:italic;
      color: #eee;
  }
  ::-moz-placeholder { /* Firefox 19+ */
    font-style:italic;
      color: #eee;
      opacity: 1;
  }
  :-moz-placeholder { /* Firefox 4 - 18 */
    font-style:italic;
      color: #eee;
      opacity: 1;
  }
  .ui.segment.header{position:relative;background:#fdfdfd;box-shadow:inset 0 -2px 1px rgba(0,0,0,0.03);}
  .header > .ui.checkbox{position:absolute;left:1em;top:1.25em;}

    input[type="checkbox"]{
        cursor: pointer;
        position: absolute;
        top: 1.25em;
        left: 1em;
        opacity: 0 !important;
        outline: 0;
        z-index: 3;
        width: 17px;
        height: 17px;
    }

    input[type="checkbox"] + label:before{
        position:absolute;
        top: 1.25em;left:1em;
        width:17px;height:17px;
        content: '';
        background:#fff;
        border-radius:.21428571rem;
        -webkit-transition: border .1s ease,opacity .1s ease,-webkit-transform .1s ease,-webkit-box-shadow .1s ease;
        transition: border .1s ease, opacity .1s ease, -webkit-transform .1s ease, -webkit-box-shadow .1s ease;
        transition: border .1s ease, opacity .1s ease, transform .1s ease, box-shadow .1s ease;
        transition: border .1s ease, opacity .1s ease, transform .1s ease, box-shadow .1s ease, -webkit-transform .1s ease, -webkit-box-shadow .1s ease;
        border: 1px solid #d4d4d5;
    }

    input[type="checkbox"] + label:after {
        position: absolute;
        font-family: Checkbox;
        font-size: 14px;
        top: 1.25em;
        left: 1em;
        width: 17px;
        height: 17px;
        text-align: center;
        opacity: 0;
        color: rgba(0,0,0,.87);
        -webkit-transition: border .1s ease,opacity .1s ease,-webkit-transform .1s ease,-webkit-box-shadow .1s ease;
        transition: border .1s ease,opacity .1s ease,-webkit-transform .1s ease,-webkit-box-shadow .1s ease;
        transition: border .1s ease,opacity .1s ease,transform .1s ease,box-shadow .1s ease;
        transition: border .1s ease,opacity .1s ease,transform .1s ease,box-shadow .1s ease,-webkit-transform .1s ease,-webkit-box-shadow .1s ease;
    }
    input[type="checkbox"]:hover + label:before{border-color:#96c8da;}
    input[type="checkbox"]:checked ~ label:after {
        content: '\e800';
        opacity: 1;
        color: rgba(0,0,0,.95);
    }
    .ui.secondary.segment .four.wide.column p{margin-top:0.65em;}
</style>
