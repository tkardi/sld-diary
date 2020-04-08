# sld-diary

This is a companion piece to
[this writeup (and maybe more later)](https://tkardi.ee/writeup/post/2020/03/20/geoserver-sld-i/)
on composing GeoServer SLD in such a way to have less SLD to write. Does that make sense?

Anyway, these are GeoServer data directory files. Expects a Postgres/PostGIS
database running on `localhost` and a database user `geoserver` with pass
`geoserver`. Substitute these for your own database as needed at
[src/data/workspaces/public/localhost/datastore.xml](../src/data/workspaces/public/localhost/datastore.xml).

Also `public.asustusyksus` table in the database. This (Estonian administrative units
[settlements layer](https://geoportaal.maaamet.ee/docs/haldus_asustus/asustusyksus_shp.zip) from
[the Estonian Land Board's](https://geoportaal.maaamet.ee/eng/Spatial-Data/Administrative-and-Settlement-Division-p312.html)
homepage) can be downloaded, unzipped and then imported with shp2pgsql.

```
~/data/tmp$ wget https://geoportaal.maaamet.ee/docs/haldus_asustus/asustusyksus_shp.zip -O asustusyksus_shp.zip
 [..]
~/data/tmp$ unzip asustusyksus_shp.zip
Archive:  asustusyksus_shp.zip
  inflating: asustusyksus_20200301.dbf  
  inflating: asustusyksus_20200301.prj  
  inflating: asustusyksus_20200301.shp  
  inflating: asustusyksus_20200301.shx
~/data/tmp$ shp2pgsql -d -s 3301 -g geom -W "cp1257" -I  asustusyksus_20200301.shp public.asustusyksus | psql -h localhost -d <dbname> -U <yourdb_user> --quiet
 [..]
~/data/tmp$
```

**Note**: this is educational material, so please pay attention not to use
plaintext passwords in your datastore.xml declarations in real life. Don't do it!
