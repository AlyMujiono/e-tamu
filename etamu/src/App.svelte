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
  import EmailIdVisit from "./pages/EmailIdVisit.svelte";
  import EmailNotifVisit from "./pages/EmailNotifVisit.svelte";
</script>

<Router>
  <Route path="admin" component={Admin} />
  <Route path="login" component={Login} />
  <Route path="registervisit" component={RegisterVisit} />
  <Route path="registervisit/verify" component={VerifyOtp} />
  <Route path="visitinfo" component={VisitInfo} />
  <Route path="admin/daftarkunjungan" component={DashboardAdmin} />
  <Route path="admin/daftaruser" component={DaftarUser} />
  <Route path="admin/buatuser" component={BuatUser} />
  <Route path="admin/visitinfo" component={VisitInfoAdmin} />
  <Route path="otpemail" component={EmailOtp} />
  <Route path="email_idvisit" component={EmailIdVisit} />
  <Route path="email_notif" component={EmailNotifVisit} />
</Router>
