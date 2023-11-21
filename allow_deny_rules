data "google_active_folder" "eng_owned" {
  display_name = "eng-owned"
  parent       = "organizations/<xxxxxxxxxxx>"
}
resource "google_computer_firewall_policy" "global_firewall_rules" {
  parent      = data.google_active_folder.eng_owned.id
  short_name  = "global firewall rules"
  description = "global firewall rules"
}
resource "google_compute_firewall_policy_rule" "deny_ssh_policy_rule" {
  firewall_policy = google_compute_firewall_policy.global_deny_rules.name
  description     = "deny default ssh"
  priority        = 9000
  direction       = "INGRESS"
  action          = "deny"
  match {
    layer4_configs {
      ip_protocol = "tcp"
      ports       = [22]
    }
    src_ip_ranges = ["0.0.0.0/0"]
  }
}
resource "google_compute_firewall_policy_rule" "deny_rdp_policy_rule" {
  firewall_policy = google_compute_firewall_policy.global_deny_rules.name
  description     = "deny default rdp"
  priority        = 9000
  direction       = "INGRESS"
  action          = "deny"
  match {
    layer4_configs {
      ip_protocol = "tcp"
      ports       = [3389]
    }
    src_ip_ranges = ["0.0.0.0/0"]
  }
}
resource "google_compute_firewall_policy_rule" "allow_iap_policy_rule" {
  firewall_policy = google_compute_firewall_policy.global_deny_rules.name
  description     = "allow IAP"
  priority        = 1000
  direction       = "INGRESS"
  action          = "allow"
  match {
    layer4_configs {
      ip_protocol = "tcp"
      ports       = [22]
    }
    src_ip_ranges = ["35.235.240.0/20"]
  }
}
resource "google_compute_firewall_policy_association" "global_firewall_policy_association" {
  firewall_policy   = google_compute_firewall_policy.global_firewall_rules.id
  name              = "global_firewall_association"
  attachment_target = data.google_active_folder.eng_owned.name
