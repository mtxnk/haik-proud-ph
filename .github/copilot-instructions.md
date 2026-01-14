# GitHub Copilot Instructions for haik.proud.ph

## 🚨🚨🚨 RULE #0 - ALWAYS USE ABSOLUTE PATHS 🚨🚨🚨

**⚠️ TERMINAL BUG**: cd ignored - use `git -C /var/www/haik-proud-ph status`

---

## 🚨 CRITICAL: LIVE PRODUCTION ENVIRONMENT

**THIS IS THE LIVE PRODUCTION WEBSITE**

- **Location**: `/var/www/haik-proud-ph/`
- **Live URL**: https://haik.proud.ph
- **Deployment**: Direct - changes are immediately live
- **Testing**: On live domain only (no localhost)

---

## 🌐 Live Site Details

- **Live URL**: https://haik.proud.ph
- **Server**: x1-mnl-pph-n1 (VM in Philippines)
- **Web Server**: Caddy (configured in `/etc/caddy/Caddyfile`)
- **Document Root**: `/var/www/haik-proud-ph/`
- **Architecture**: Static HTML academic monograph

---

## 🛡️ Security & Caching Best Practices

**CRITICAL:** Always follow these patterns (see `/var/www/.github/instructions/security-caching.instructions.md`):

1. **CSP Security:** Static HTML page - keep external resources minimal
2. **Cache-Control Headers:** Add to Caddy if updates not appearing:
   ```caddyfile
   header /*.html Cache-Control "no-cache, no-store, must-revalidate, max-age=0"
   ```
3. **Asset Versioning:** Use query strings for cache-busting if needed

**Mobile browsers cache aggressively** - explicit Cache-Control headers prevent stale pages!

---

## 🛠️ Development Workflow

### Making Changes
1. **Edit files directly** in `/var/www/haik-proud-ph/`
2. **Test by viewing** https://haik.proud.ph
3. **Commit changes** with descriptive messages
4. **Push to main branch** - changes are immediately live

### Testing Protocol
```bash
# ✅ CORRECT: Test directly on live site
curl -s https://haik.proud.ph | head -20

# ❌ WRONG: No localhost testing needed
```

---

## 📁 File Structure

```
/var/www/haik-proud-ph/
├── index.html            # Academic monograph on Haik
├── .github/
│   └── copilot-instructions.md  # This file
└── README.md             # (Optional) Project documentation
```

---

## 🎯 Project Purpose

**Academic Monograph Website**: Haik, the Benevolent Sea God of the Tagalog World

- **Content Type**: Citizen-science research paper
- **Author**: Nik Metaxa-Schwarten
- **Topic**: Philippine mythology, ocean deities, cultural preservation
- **Audience**: Researchers, educators, ocean literacy advocates

---

## 🎨 Design Principles

- **Academic Typography**: Georgia serif for scholarly readability
- **Structured HTML**: Semantic article, section, header tags
- **Professional Styling**: Ocean-themed color palette (blues, grays)
- **Mobile-First**: Responsive design for all devices
- **Print-Optimized**: Clean CSS for academic printing
- **Accessibility**: Proper heading hierarchy, alt text, semantic markup

---

## 📚 Content Guidelines

### When Updating Content:
- **Maintain academic tone** - formal, evidence-based writing
- **Cite sources** - all claims must have bibliographic support
- **Preserve structure** - keep existing section organization
- **Add metadata** - update Open Graph tags if title/description changes
- **Verify links** - check all external bibliography URLs work

### Adding New Resources:
- Place in appropriate category (Academic, General, Media)
- Include descriptive explanation below each link
- Maintain consistent formatting

---

## 🔧 Caddy Configuration

**Location**: `/etc/caddy/Caddyfile`

**Required Configuration**:
```caddy
haik.proud.ph {
    encode gzip
    root * /var/www/haik-proud-ph
    file_server
    
    # Optional: Cache control for updates
    header /*.html Cache-Control "no-cache, no-store, must-revalidate, max-age=0"
}
```

**Deployment Steps**:
1. Add configuration to Caddyfile
2. Validate: `sudo caddy validate --config /etc/caddy/Caddyfile`
3. Reload: `sudo systemctl reload caddy`
4. Test: `curl -I https://haik.proud.ph`

---

## 📞 Quick Reference

| Action | Command |
|--------|---------|
| Test site access | `curl -s https://haik.proud.ph \| head -20` |
| Check Caddy config | `sudo caddy validate --config /etc/caddy/Caddyfile` |
| Reload Caddy | `sudo systemctl reload caddy` |
| View Caddy logs | `sudo journalctl -u caddy -f` |
| Git status | `git -C /var/www/haik-proud-ph status` |
| Sync submodule | `/var/www/0-mnl-scrpt/xGITmanager/subsync.sh` |

---

## 🔒 System Files (Require sudo)

**✅ CORRECT**: `sudo nano /etc/caddy/Caddyfile` or `sudo sed -i 's/old/new/' /etc/caddy/Caddyfile`
**❌ WRONG**: Editing without sudo (Permission Denied)

**WORKFLOW:**
1. Backup: `sudo cp /etc/caddy/Caddyfile /etc/caddy/Caddyfile.backup-$(date +%Y%m%d-%H%M%S)`
2. Edit with sudo
3. Validate: `sudo caddy validate --config /etc/caddy/Caddyfile`
4. Reload: `sudo systemctl reload caddy`

---

**Remember**: This is a live production academic website. Maintain scholarly standards and test thoroughly before deployment.
