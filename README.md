# Fixed-Sized Thumbnail Grid

This is an example of a site displaying fixed-sized thumbnails in a grid. The media queries of the width are
generated with Sass, so the grid aways fits perfectly into the site..

`style.scss`

    /* the outer left and right padding is needed for the calculation */
    $site-padding: 15;
    /* the thumbnail width */
    $thumbnail-width: 96;
    /* the thumbnail margin */
    $thumbnail-margin: 5;
    /* minimum thumbnails per row */
    $min-per-row: 3;
    /* maximum thumbnails per row */
    $max-per-row: 9;

    .site {
      /* site is centered */
      margin: 0 auto;
      padding-left: $site-padding + px;
      padding-right: $site-padding + px;

      .thumbnail-container {
        /* add some margin to the navbar */
        margin-top: 40px;
        /* subtract the thumbnail margin on the left */
        margin-left: -$thumbnail-margin + px;
        /* subtract the thumbnail margin on the right */
        margin-right: -$thumbnail-margin +px;
        /* remove all text so the calculation works */
        font-size: 0;

        /* clearfix */
        &:after {
          content: "";
          display: table;
          clear: both;
        }

        .thumbnail {
          /* Bootstrap override */
          padding: 0;
          /* thumbnails float left */
          float: left;
          width: $thumbnail-width + px;
          margin: $thumbnail-margin + px;
        }
      }
    }

    @for $i from $min-per-row through $max-per-row {
      /* all thumbnails plus margin */
      $main-width: ($thumbnail-width * $i) + ($thumbnail-margin * 2 * ($i - 1));
      /* the thumbnail with plus site padding */
      $site-width: $main-width + $site-padding * 2;
      /* the site width plus offset */
      $media-width: if($i > $min-per-row, $site-width + 30, 0);

      @media (min-width: $media-width + px) {
        .site {
          width: $site-width + px;

          .main {
            width: $main-width + px;
          }
        }
      }
    }