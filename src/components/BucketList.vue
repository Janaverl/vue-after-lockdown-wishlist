<template>
  <div class="row justify-content-center">
    <div class="col-sm-10 col-md-8 col-md-6 col card">
        <div class="card-header row">
          <div class="col-sm-8"><h2><b>10 things I will do when Lockdown COVID-19 is over.</b></h2></div>
          <div class="col-sm-4">
              <button type="button" class="btn btn-success add-new float-right"><i class="fa fa-plus"></i> Add New</button>
          </div>
        </div>
        <div class="card-body">
          <div class="progress card-title">
            <div class="progress-bar progress-bar-striped bg-success" style="width: 10%">1</div>
          </div>
          <table class="table table-bordered">
              <thead>
                <tr>
                  <th style="width: 20%">name</th>
                  <th style="width: 60%">description</th>
                  <th style="width: 20%">Actions</th>
                </tr>
              </thead>
              <tbody>
                  <tr>
                      <td class="font-weight-bold">example</td>
                      <td>Mijn goede vriendin Jana uitnodigen voor een BBQ.</td>
                      <td>
                        <a class="edit text-warning p-3"><i class="far fa-edit"></i></a>
                        <a class="delete text-danger p-3"><i class="far fa-trash-alt"></i></a>
                      </td>
                  </tr>
                  <tr>
                    <td><input type="text" class="form-control" name="name"></td>
                    <td><input type="text" class="form-control" name="description"></td>
                    <td>
                        <a class="add text-success p-3"><i class="far fa-plus-square"></i></a>
                        <a class="delete text-danger p-3"><i class="far fa-trash-alt"></i></a>
                    </td>  
                  </tr>    
              </tbody>
          </table>
        </div>
    </diV>
  </div>
</template>

<script>
  export default {
    name: 'BucketList'
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
