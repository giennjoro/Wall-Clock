<script>
  import Example from './Example.svelte'
  let name = '<b style="color:green">George</b> Njoroge',
    age = '<i>22</i>'
</script>

<style>
  this-tag {
    text-align: center;
    padding: 1em;
    max-width: 240px;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }

  @media (min-width: 640px) {
    this-tag {
      max-width: none;
    }
  }
</style>

<this-tag>
  <h1>
    I am
    {@html name}
    !
  </h1>
  <h3>
    My age is
    {@html age}
  </h3>
</this-tag>
<Example profession="Developer" />
