<script>
  import Login from './pages/Login.svelte';
  import { Router, Link, Route } from "svelte-routing";
  import Admin from './pages/Admin.svelte';
  import RegisterVisit from './pages/RegisterVisit.svelte';
</script>

<Router>
  <div>
    <Route path="admin" component={Admin}/>
    <Route path="login" component={Login}/>
    <Route path="registerVisit" component={RegisterVisit}/>
  </div>
</Router>