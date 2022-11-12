<script>
  import Login from "./pages/Login.svelte";
  import { Router, Link, Route } from "svelte-routing";
  import Admin from "./pages/Admin.svelte";
  import RegisterVisit from "./pages/RegisterVisit.svelte";
  import VerifyOtp from "./pages/VerifyOTP.svelte";
  import VisitInfo from "./pages/VisitInfo.svelte";
  import DashboardAdmin from "./pages/DashboardAdmin.svelte";
  import DaftarUser from "./pages/DaftarUser.svelte";
  import BuatUser from "./pages/BuatUser.svelte";
  import VisitInfoAdmin from "./pages/VisitInfoAdmin.svelte";
  import EmailOtp from "./pages/EmailOTP.svelte";
</script>

<Router>
  <Route path="admin" component={Admin} />
  <Route path="login" component={Login} />
  <Route path="registervisit" component={RegisterVisit} />
  <Route path="registervisit/verify" component={VerifyOtp} />
  <Route path="visitinfo" component={VisitInfo} />
  <Route path="dashboardadmin" component={DashboardAdmin} />
  <Route path="daftaruser" component={DaftarUser} />
  <Route path="buatuser" component={BuatUser} />
  <Route path="visitinfoadmin" component={VisitInfoAdmin} />
  <Route Path="email_otp" component={EmailOtp} />
</Router>
