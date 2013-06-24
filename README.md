XBMC Repository Tools
=====

Two tools are currently available.

build_xbmc_zip.py
-----------------

This script can be used to generate an XBMC compliant ZIP file ready for either
uploading to the web, or for use in an XBMC repository.

This script must be run the working directory of an XBMC Add-on.

Currently the script will output two ZIP files in the current directory. 
The first excludes the directory `resources/lib/deps/`, where it is expected
that the resulting ZIP file will be added to an XBMC repsitory where
dependencies like BeautifulSoup will be avilable.

The second will include the `resources/lib/deps/` directory and will be
suitable for downloading and adding directly into XBMC. It will identified by
the _deps suffix to the ZIP file.

The filename of the ZIP file is automatically generated by the content in the
addon.xml file which is required for the addon. 

For example:
  - plugin.video.abc_iview-1.3.1.zip
  - plugin.video.abc_iview-1.3.1_deps.zip

git-hooks/pre-commit
--------------------

This file is a GIT pre-commit script which should be symlinked into your GIT
hooks directory.

For example (run from your addon working directory):
`ln -s ../tools/git-hooks/pre-commit .git/hooks/pre-commit`

This script does two main things; it generates an XBMC compliant changelog.txt
and updates the version number within the addon.xml and
`resources/lib/version.py` for use within the addon.

The version number generated by this script is obtained from the GIT history
and tags.

When you intend to create a stable release of your addon, you must tag your
release in GIT like this (for example, version 1.3.1)

`git tag -a v1.3.1 -m 'version 1.3.1'`

The script will then use this version number for writing into the addon.xml
file. For commits which are not stable releases, the version number will be
in the format:

`(last.tagged.release)-(number-of-commits-since-last-tag)-(git hash)`

For example:

`1.3.1-6-g65535a9`
