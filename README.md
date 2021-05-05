# Dotnet Reviewdog Action

Analyzes a dotnet build log file to verify the code style

## Usage

```yaml
    steps:
    - uses: actions/checkout@v2
    - uses: actions/setup-dotnet@v1
      with:
         dotnet-version: 3.1.x
    - run: echo "::remove-matcher owner=csc::"
    - uses: reviewdog/action-setup@v1
    - run: dotnet restore
    - run: dotnet build -c Release --no-restore | tee dotnet.buildlog
    - uses: SamhammerAG/dotnet-reviewdog-action@v1
      with:
        name: dotnet
        build_log_file: dotnet.buildlog
        line_exclude_regex: ".*(warning|error) CS0618:.*"
        github_token: ${{ secrets.MY_TOKEN }}
        level: error
        reporter: github-pr-review
        fail_on_error: false
        reviewdog_flags: "-additional-flag"
        workdir: "."
```

### Arguments
* name: Optional. The name of the job that is added to your workflow. Default is dotnet.
* build_log_file: Optional. The file that is analyzed. Default is dotnet.buildlog.
* line_exclude_regex: Optional. Exclude specific warnings by a regex. Default is empty.
* github_token: Optional. Default is github.token.
* level: Optional. Report level for reviewdog [info,warning,error]. Default is error.
* reporter: Optional. Reporter of reviewdog command [github-pr-check,github-check,github-pr-review]. Default is github-pr-review.
* fail_on_error: Optional. Exit code for reviewdog when errors are found [true,false] Default is false.
* reviewdog_flags: Optional. Additional reviewdog flags
* workdir: Optional. The directory from which to look for the build log file and run reviewdog. Default '.'

## License

This project is distributed under the [MIT license](LICENSE.md).
