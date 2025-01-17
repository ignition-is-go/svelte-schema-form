<script lang="ts">
  import type { CommonComponentParameters } from './types/CommonComponentParameters'
  import { editorForSchema } from './types/schema'
  interface Props {
    params: CommonComponentParameters
    schema: any
    value: any
  }

  let { params, schema = $bindable(), value }: Props = $props()
  let components = $derived(params.components)
  let pathComponents = $derived(params.pathComponents)
  let path = $derived(params.path)
  let typeComponent: any

  let Component: new (...args: any[]) => any = $derived(
    pathComponents?.[path.join('.')] ?? components[editorForSchema(schema)],
  )
</script>

<Component {params} {value} bind:schema></Component>
