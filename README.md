## HuggingFface Deployment Guide

Hugging Face video tutorial link: https://youtu.be/XERxg9AODeo

1. fork This project
2. Allow the "I understand my workflows, go ahead and enable them" button in the Actions menu.
3. After filling in the necessary variables in index.js within the hug branch, obfuscate and save it. The JavaScript obfuscation address is: https://obfuscator.io
4. Modify the image name in .github/workflows/build-hug-image.yml 44
5. Create an empty space on the hookface using Docker.
6. Create a new file named `Dockerfile` with the following content:
```
FROM ghcr.io/githubusername/mirrorname:latest

ENV DOMAIN=space domain
```

* PaaS Platform environment variables
  | variable name        | Is it necessary? | default value | Remark |
  | ------------ | ------ | ------ | ------ |
  | UUID         | no |de04add9-5c68-6bab-950c-08cd5320df33| Nezha v1 has been enabled. Please modify the UUID.|
  | PORT         | no |  7860  |  Listening port                    |
  | NEZHA_SERVER | no |        | Nezha v1 form：nz.abc.com:8008   Nezha v0 form：nz.abc.com|
  | NEZHA_PORT   | no |        | Nezha v1 does not have this variable, v0/s agent port | 
  | NEZHA_KEY    | no |        | Nezha v1/s NZ_CLIENT_SECRET or v0/s agent port |
  | NAME         | no |        | Node name prefixes, for example: Glitch |
  | DOMAIN       | yes |        | The domain name assigned to the project or the domain name that has been reverse-proxied, excluding https://prefix  |
  | SUB_PATH     | no |  sub   | Subscription path   |
  | AUTO_ACCESS  | no |  true | Enable automatic access keep-alive (false for off, true for on). The DOMAIN variable must also be specified.|

* domain name/${SUB_APTH}View node information, non-standard ports, domain:port/${SUB_APTH}

### Use Cloudflare workers or snippets to reverse proxy domains to add CDN acceleration to nodes.
```
export default {
    async fetch(request, env) {
        let url = new URL(request.url);
        if (url.pathname.startsWith('/')) {
            var arrStr = [
                'your-space.domain', // Enter your spoofed domain name within these single quotes.
            ];
            url.protocol = 'https:'
            url.hostname = getRandomArray(arrStr)
            let new_request = new Request(url, request);
            return fetch(new_request);
        }
        return env.ASSETS.fetch(request);
    },
};
function getRandomArray(array) {
  const randomIndex = Math.floor(Math.random() * array.length);
  return array[randomIndex];
}
```

## Open source license description (based on GPL)

This project is released under the GNU General Public License (GPL) and includes the following instructions.：

1. You are free to use, copy, modify and distribute the source code of this project, provided that you retain the original author/s information and the contents of this agreement;
2. The modified version must also be open source under the same license;
3. **This project or any part thereof may not be used for commercial purposes without the express authorization of the original author.**

Commercial uses include, but are not limited to:
- Embed this project into the software, system, or service you are selling;
- Profit directly or indirectly from this project (e.g., through advertising, SaaS services, etc.).
- Used as a business tool within a company or organization.

For commercial licensing, please contact the original author:[admin@eooce.com]

all rights reserved ©2025 `eooce`
