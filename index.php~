<?php
if(!empty($_POST)){
    $blacklist=json_decode(file_get_contents("list.json"),true);
    if (filter_var($_POST['ip'], FILTER_VALIDATE_IP)) {
        $ip=explode('.',$_POST['ip']);
    } else {
        $dns=dns_get_record($_POST['ip'], DNS_A);
        $ip=explode('.',$dns[0]['ip']);
    }
    $reverse=$ip[3].'.'.$ip[2].'.'.$ip[1].'.'.$ip[0];
}
?>
<!doctype html>
<html lang="en" class="h-100">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
    <meta name="description" content="">
    <meta name="author" content="Louis Ouellet, https://github.com/LouisOuellet">
    <title>Blacklist Check</title>

    <!-- Bootstrap core CSS -->
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.4.1/css/bootstrap.min.css" integrity="sha384-Vkoo8x4CGsO3+Hhxv8T/Q5PaXtkKtu6ug5TOeNV6gBiFeWPGFN9MuhOf23Q9Ifjh" crossorigin="anonymous">
    <style>
      .bd-placeholder-img {
        font-size: 1.125rem;
        text-anchor: middle;
        -webkit-user-select: none;
        -moz-user-select: none;
        -ms-user-select: none;
        user-select: none;
      }

      @media (min-width: 768px) {
        .bd-placeholder-img-lg {
          font-size: 3.5rem;
        }
      }
    </style>
    <!-- Custom styles for this template -->
    <link href="sticky-footer-navbar.css" rel="stylesheet">
  </head>
  <body class="d-flex flex-column h-100">
    <header>
      <!-- Fixed navbar -->
      <nav class="navbar navbar-expand-md navbar-dark fixed-top bg-dark">
        <a class="navbar-brand" href="index.php">Blacklist Check</a>
        <div class="navbar-collapse">
          <ul class="navbar-nav mr-auto">
            <li class="nav-item active">
              <a class="nav-link" href="https://github.com/LouisOuellet/Blacklist">GitHub</a>
            </li>
          </ul>
        </div>
      </nav>
    </header>

    <!-- Begin page content -->
    <main role="main" class="flex-shrink-0">
      <div class="container pt-5">
        <h1 class="mt-5">Blacklist Check</h1>
        <p class="lead">This PHP code checks an IP/FQDN against a list of public blacklist.</p>
      </div>
      <form method="post">
          <div class="container">
            <div class="row pb-2">
                <div class="col-md-12">
                    <div class="form-group">
                        <div class="input-group">
                            <div class="input-group-prepend"><span class="input-group-text">IP/FQDN</span></div>
                            <input type="text" id="ip" name="ip" class="form-control" placeholder="" value="<?php if(isset($_POST['ip'])){ echo $_POST['ip']; } ?>">
                            <button type="submit" name="Check" class="form-control btn btn-primary col-md-2">Check</button>
                        </div>
                    </div>
                </div>
            </div>
          </div>
          <?php if((!empty($_POST))&&(isset($_POST['Check']))){?>
              <div class="container" style="padding:25px;">
                  <div class="row">
                      <table class="table table-striped table-bordered table-hover table-sm">
                        <thead class="thead-dark">
                          <tr>
                              <th>Blacklist</th>
                              <th>Result</th>
                              <th>TTL</th>
                          </tr>
                        </thead>
                        <tbody>
                          <?php foreach($blacklist['lists'] as $list){?>
                              <?php $dns=@dns_get_record($reverse.'.'.$list, DNS_A); ?>
                              <tr>
                                  <td><?= $list?></td>
                                  <td>
                                    <?php if(empty($dns)){ ?>
                                        <span class="badge badge-success">Not Listed</span>
                                    <?php } else { ?>
                                        <span class="badge badge-danger">Listed</span>
                                    <?php } ?>
                                  </td>
                                  <td><?php if(!empty($dns)){ echo $dns[0]['ttl']; } ?></td>
                              </tr>
                          <?php } ?>
                        </tbody>
                      </table>
                  </div>
              </div>
          <?php } ?>
      </form>
    </main>

    <footer class="footer mt-auto py-3" style="padding:10px;background-color:#ccc;">
      <div class="float-right d-none d-sm-block">
        <b>Version</b> 1.1-0
      </div>
      <strong>Copyright &copy; 2020-<?= date('Y') ?> <a href="https://laswitchtech.com">LaswitchTech</a>.</strong> All rights reserved.
    </footer>
    <script src="https://code.jquery.com/jquery-3.4.1.slim.min.js" integrity="sha384-J6qa4849blE2+poT4WnyKhv5vZF5SrPo0iEjwBvKU7imGFAV0wwj1yYfoRSJoZ+n" crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.0/dist/umd/popper.min.js" integrity="sha384-Q6E9RHvbIyZFJoft+2mJbHaEWldlvI9IOYy5n3zV9zzTtmI3UksdQRVvoxMfooAo" crossorigin="anonymous"></script>
    <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.4.1/js/bootstrap.min.js" integrity="sha384-wfSDF2E50Y2D1uUdj0O3uMBJnjuUD4Ih7YwaYd1iqfktj0Uod8GCExl3Og8ifwB6" crossorigin="anonymous"></script>
</html>
