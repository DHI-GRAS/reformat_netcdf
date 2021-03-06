## Running the script

See usage information with
```
python convert.py --help
```


## Building the executable

Make sure you have a `convert.spec` file that looks like this:

```
    # -*- mode: python -*-

    block_cipher = None


    a = Analysis(['convert.py'],
                 binaries=None,
                 datas=None,
                 hiddenimports=[
                    'six', 'packaging', 
                    'packaging.version', 'packaging.specifiers', 'packaging.requirements', 
                    'scipy.linalg', 'scipy.integrate', 'appdirs'],
                 hookspath=[],
                 runtime_hooks=[],
                 excludes=[],
                 win_no_prefer_redirects=False,
                 win_private_assemblies=False,
                 cipher=block_cipher)
    pyz = PYZ(a.pure, a.zipped_data,
                 cipher=block_cipher)
    exe = EXE(pyz,
              a.scripts,
              a.binaries,
              a.zipfiles,
              a.datas,
              name='convert',
              debug=False,
              strip=False,
              upx=True,
              console=True )
```

and have all the modules listed in `hiddenimports` installed on your system (`conda install packaging appdirs scipy`). Then you can build the binary with

    pyinstaller -F convert.spec
