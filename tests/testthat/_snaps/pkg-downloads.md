# new_pkg_download_proposal

    Code
      dl
    Output
      <pkg_download_proposal>
      + refs:
        - pkg3
      (use `$resolve()` to resolve dependencies)

---

    Code
      dl$get_refs()
    Output
      [1] "pkg3"

---

    Code
      sort(dl$get_config()$list())
    Output
       [1] "bioconductor_mirror"   "bioconductor_version"  "build_vignettes"      
       [4] "cache_dir"             "cran_mirror"           "dependencies"         
       [7] "library"               "metadata_cache_dir"    "metadata_update_after"
      [10] "package_cache_dir"     "platforms"             "r_versions"           
      [13] "sysreqs"               "sysreqs_dry_run"       "sysreqs_rspm_repo_id" 
      [16] "sysreqs_rspm_url"      "sysreqs_sudo"          "sysreqs_verbose"      
      [19] "use_bioconductor"      "windows_archs"        

---

    Code
      dl
    Output
      <pkg_download_proposal>
      + refs:
        - pkg3
      + has resolution (+2 dependencies)
      (use `$download()` to download packages)
      (use `$get_resolution()` to see resolution results)

---

    Code
      dl$get_resolution()[, c("ref", "type", "directpkg", "package", "error")]
    Output
      # A data frame: 3 x 5
        ref   type     directpkg package error     
        <chr> <chr>    <lgl>     <chr>   <list>    
      1 pkg1  standard FALSE     pkg1    <list [0]>
      2 pkg2  standard FALSE     pkg2    <list [0]>
      3 pkg3  standard TRUE      pkg3    <list [0]>

# async_resolve

    Code
      synchronize(dl$async_resolve()$then(function() "done"))
    Output
      [1] "done"

---

    Code
      dl$get_resolution()[, c("ref", "type", "directpkg", "package", "error")]
    Output
      # A data frame: 3 x 5
        ref   type     directpkg package error     
        <chr> <chr>    <lgl>     <chr>   <list>    
      1 pkg1  standard FALSE     pkg1    <list [0]>
      2 pkg2  standard FALSE     pkg2    <list [0]>
      3 pkg3  standard TRUE      pkg3    <list [0]>

# download

    Code
      dir(tmp, recursive = TRUE, pattern = "[.]tar[.]gz$")
    Output
      [1] "src/contrib/pkg1_1.0.0.tar.gz" "src/contrib/pkg2_1.0.0.tar.gz"
      [3] "src/contrib/pkg3_1.0.0.tar.gz"

# async_download

    Code
      dir(tmp, recursive = TRUE, pattern = "[.]tar[.]gz$")
    Output
      [1] "src/contrib/pkg1_1.0.0.tar.gz" "src/contrib/pkg2_1.0.0.tar.gz"
      [3] "src/contrib/pkg3_1.0.0.tar.gz"

---

    Code
      dl$get_downloads()$target
    Output
      [1] "src/contrib/pkg1_1.0.0.tar.gz" "src/contrib/pkg2_1.0.0.tar.gz"
      [3] "src/contrib/pkg3_1.0.0.tar.gz"

