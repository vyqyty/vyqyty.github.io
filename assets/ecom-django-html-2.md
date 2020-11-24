---
<!DOCTYPE html>
<html lang="vi">
    <head>
        <meta charset="UTF-8">
        <title>Ecom</title>
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <link href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u" crossorigin="anonymous">
        <link href="https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css" rel="stylesheet" integrity="sha384-wvfXpqpZZVQGK6TAh5PVlGOfQNHSoD2xbE+QkPxCAFlNEevoEH3Sl0sibVcOQVnN" crossorigin="anonymous">
        <link href="https://maxcdn.bootstrapcdn.com/bootswatch/3.3.7/cosmo/bootstrap.min.css" rel="stylesheet" integrity="sha384-h21C2fcDk/eFsW9sC9h0dhokq5pDinLNklTKoxIZRUn3+hvmgQSffLLQ4G4l2eEr" crossorigin="anonymous">
    </head>
    
    <script defer src="https://code.jquery.com/jquery-3.2.1.min.js" integrity="sha256-hwg4gsxgFZhOsEEamdOYGBf13FyQuiTwlAQgxVSNgt4=" crossorigin="anonymous"></script>
    <script defer src="https://cdnjs.cloudflare.com/ajax/libs/twitter-bootstrap/3.3.7/js/bootstrap.min.js"></script>

    <body>
        <nav class="navbar navbar-default navbar-expand-sm" style="background-color: #212121;">
          <div class="container-fluid">
            <div class="navbar-header">
              <a class="navbar-brand" href="/">Django Ecom</a>
            </div>
            <div class="collapse navbar-collapse" id="navbar-items">
            <ul class="nav navbar-nav">   
            </ul>    
            <ul class="nav navbar-nav navbar-right">
                <li><span class="navbar-brand slogan">Welcome to Django</span></li>
                <li>
                      <form class="navbar-form navbar-left" role="search">
                        <div class="form-group">
                          <input type="text" class="form-control" placeholder="Search">
                        </div>
                        <button type="submit" class="btn btn-default">Submit</button>
                      </form>
                </li>
            </ul>
            </div>
          </div>
        </nav>
        
        <div class="container">
        <div class="col-sm-8">
            <div class="row">
                <div class="col-xs-6">
                    <a href="{% url 'product' product.id %}"><img src="/media/{{ product.image }}" /></a>
                </div>
                <div class="col-xs-3">
                    <b>Product Name</b><br/>
                    <b>Price</b><br/>
                    <b>Quantity</b><br/>
                    <b>Description</b><br/>
                </div>
                <div class="col-xs-3">
                    {{product.name}}<br/>
                    ${{product.price}}<br/>
                    {{product.quantity}}<br/>
                    {{product.description}}<br/>
                </div>
            </div>
        </div>
        <div class="col-sm-4">
        </div>
        </div>
    </<body>
</html>
---
