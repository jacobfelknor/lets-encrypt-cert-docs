# lets-encrypt-cert-docs

Based on https://www.digitalocean.com/community/tutorials/how-to-acquire-a-let-s-encrypt-certificate-using-dns-validation-with-acme-dns-certbot-on-ubuntu-18-04

```bash
# install certbot
sudo apt-add-repository ppa:certbot/certbot
sudo apt install certbot

# set up DNS validation
wget https://github.com/joohoi/acme-dns-certbot-joohoi/raw/master/acme-dns-auth.py
# if above not available, I've included a copy of the file in this repo
chmod +x acme-dns-auth.py
vim acme-dns-auth.py # add python3 at end
sudo mv acme-dns-auth.py /etc/letsencrypt/

# get cert
sudo certbot certonly --manual --manual-auth-hook /etc/letsencrypt/acme-dns-auth.py --preferred-challenges dns --debug-challenges -d \*.your-domain -d your-domain
# add specified DNS entries
# Should be good! For ex,
# Certificate is saved at: /etc/letsencrypt/live/jacobfelknor.com/fullchain.pem
# Key is saved at:         /etc/letsencrypt/live/jacobfelknor.com/privkey.pem

# Renew Dry Run
sudo certbot renew --dry-run

# Renew
sudo certbot renew

```
