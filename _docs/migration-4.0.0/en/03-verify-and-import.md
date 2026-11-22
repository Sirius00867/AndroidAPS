# Step 3 · Check the version and import if needed

## Check the version

Open the menu (☰) at the top left and select **About**. It should say 4.0.0.

## Do you need to import?

The official wiki does not give a single answer:

- The update manual ([UpdateToNewVersion](https://androidaps.readthedocs.io/en/latest/Maintenance/UpdateToNewVersion.html)) says, after installing: *"make sure you have imported your settings"*.
- The backup page ([ExportImportSettings](https://androidaps.readthedocs.io/en/latest/Maintenance/ExportImportSettings.html)) says that when you update with an APK built with the same keystore *"you should not need to follow this process"*.

They fit together if what matters is the result: your settings must be there. When you install over the old app with the same keystore, they stay on the phone, and 4.0.0 converts the old names on start-up. Review your settings (steps 5 and 6). If anything is missing, or if you prefer to follow the update manual to the letter, import the step 1 export.

Importing on the same phone is safe as long as you leave **Also replace pump settings** unticked. An import is a **merge**: it only writes values that change, leaves settings missing from the file untouched and never deletes anything.

If you had to install from scratch (another phone, new keystore or uninstall), importing is required.

## How to import on 4.0.0

1. Menu (☰) → **Maintenance**. Under **File management**, pick the source with the **Local** or **Cloud** chip and tap **Import settings**. The newest file is at the top.
2. Pick the file, enter the master password and tap **Decrypt & Review**.
3. Decide on **Also replace pump settings**:
   - **Unticked (default):** your current pump, its pairing and its settings on this phone are kept. That is right when updating on the same phone, especially with a running pod.
   - **Ticked:** only when a new phone is taking over the same pump.
4. Tap **Import**. AAPS asks **Apply imported settings?** and writes nothing until you tap **OK**. **Cancel** leaves the phone unchanged.
5. Settings apply without restarting the app; only plugins whose settings changed restart. If the pump is busy, AAPS waits and offers a retry after one minute. Any treatment queued during the import is dropped and reported as cancelled.

## New phone

Install the APK first and select the AAPS directory again. If AAPS loses access to the directory (after a reinstall or clearing storage), it shows a notification and stops saving settings until you reselect it. With Dana RS you must pair the new phone and the pump manually.

Next: [Step 4 · The new interface](04-new-interface.md)
