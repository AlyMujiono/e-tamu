<script>
  import Login from "./pages/Login.svelte";
  import { Router, Link, Route } from "svelte-routing";
  import Admin from './pages/Admin.svelte';
  import RegisterVisit from './pages/RegisterVisit.svelte';
  import VerifyOtp from './pages/VerifyOTP.svelte';
  import VisitInfo from './pages/VisitInfo.svelte';
</script>

<Router>
    <Route path="admin" component={Admin} />
    <Route path="login" component={Login} />
    <Route path="registervisit" component={RegisterVisit} />
    <Route path="registervisit/verify" component={VerifyOtp} />
    <Route path="visitinfo" component={VisitInfo} />
</Router>
