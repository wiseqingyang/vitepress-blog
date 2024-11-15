<script setup>
import { data } from './allPosts.data.ts'
</script>

<ul>
  <li v-for="item in data">
    <a :href="item.url">{{item.url}}</a>
  </li>
</ul>

<pre> {{data}} </pre>

