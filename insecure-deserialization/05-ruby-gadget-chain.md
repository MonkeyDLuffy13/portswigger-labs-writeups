# Lab 05 — Exploiting Ruby deserialization using a documented gadget chain

> **Expert** · [Official lab](https://portswigger.net/web-security/deserialization/exploiting/lab-deserialization-exploiting-ruby-deserialization-using-a-documented-gadget-chain)

**Entry point:** the session cookie is a Base64 **marshaled Ruby object**.

## Solution

1. Log in (`wiener:peter`) and confirm the marshaled-Ruby session cookie.
2. Grab the published *"Universal Deserialisation Gadget for Ruby 2.x-3.x"*
   (vakzz / devcraft.io) payload-generation script.
3. Modify it: execute `rm /home/carlos/morale.txt` instead of `id`, and end
   the script with:

```ruby
puts Base64.encode64(payload)
```

4. Run it — the output is your malicious cookie.
5. In Repeater, replace the session cookie (URL-encode it) and send — the
   deserialized gadget executes the command — lab solved.

## Notes

Ruby's `Marshal.load` on untrusted data is RCE-by-default when common gems
are loaded; the universal chain needs no special framework.
