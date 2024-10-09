### Installation instructions

1. Run KIAUH and uninstall klipper (ONLY klipper)
2. In KIAUH folder create file named klipper_repos.txt and add these 2 lines:

```text
https://github.com/Klipper3d/klipper
https://github.com/0xD34D/klipper_ender3_v3_se
```

3. Then in KIAUH settings change klipper repo to this repos.
4. Install klipper in KIAUH as usual
5. Once installed build firmware as usual from the klipper folder
6. Flash the firmware to printer
7. Create prtouch.cfg with contents from [config repo](https://github.com/0xD34D/ender3-v3-se-klipper-config/blob/main/prtouch.cfg)
8. In existing printer.cfg add line [include prtouch.cfg]
9. Restart klipper service
10. PRTOUCH_PROBE_ZOFFSET should now work and return Z-offset in the end of printer.cfg

When running PRTOUCH_PROBE_ZOFFSET be ready to abort if thing go wrong.