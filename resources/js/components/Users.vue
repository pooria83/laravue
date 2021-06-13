<template>
    <div class="container p-2">
        <div class="row justify-content-center">
            <div class="col-12">
                <div class="card">
                    <div class="card-header">
                        <h3 class="card-title">Users Table</h3>

                        <div class="card-tools">
                            <button
                                class="btn btn-info"
                                data-toggle="modal"
                                data-target="#addUserModalCenter"
                            >
                                <i class="fa fa-plus mr-1"></i> Add User
                            </button>
                        </div>
                    </div>
                    <!-- /.card-header -->
                    <div class="card-body table-responsive p-0">
                        <table class="table table-hover text-nowrap">
                            <thead>
                                <tr>
                                    <th>First Name</th>
                                    <th>Email</th>
                                    <th>Action</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr v-for="user in users" :key ="user.id">
                                    <td>{{ user.name }}</td>
                                    <td>{{ user.email }}</td>
                                    <td>
                                        <i class="fa fa-edit orange"></i> |
                                        <i class="fa fa-trash red"></i>
                                    </td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                    <!-- /.card-body -->
                </div>
                <!-- /.card -->
            </div>
        </div>
        <!-- Modal -->
        <div
            class="modal fade"
            id="addUserModalCenter"
            tabindex="-1"
            role="dialog"
            aria-labelledby="addUserModalCenterTitle"
            aria-hidden="true"
        >
            <div class="modal-dialog modal-dialog-centered" role="document">
                <div class="modal-content">
                    <div class="modal-header">
                        <h5 class="modal-title" id="addUserModalLongTitle">
                            Modal title
                        </h5>
                        <button
                            type="button"
                            class="close"
                            data-dismiss="modal"
                            aria-label="Close"
                        >
                            <span aria-hidden="true">&times;</span>
                        </button>
                    </div>

                        <form
                            @submit.prevent="addUser"
                            @keydown="form.onKeydown($event)"
                        >
                          <div class="modal-body">
                        <label for="name">Name</label>
                            <input
                                v-model="form.name"
                                type="text"
                                name="name"
                                placeholder="name"
                                class="form-control"
                            />
                            <div
                                v-if="form.errors.has('name')"
                                v-html="form.errors.get('name')"
                            />
                            <label for="email">Email</label>
                             <input
                                v-model="form.email"
                                type="email"
                                name="email"
                                placeholder="email"
                                 class="form-control"
                            />
                            <div
                                v-if="form.errors.has('email')"
                                v-html="form.errors.get('email')"
                            />
                             <label for="password">Password</label>
                             <input
                                v-model="form.password"
                                type="password"
                                name="password"
                                placeholder="password"
                                 class="form-control"
                            />
                            <div
                                v-if="form.errors.has('password')"
                                v-html="form.errors.get('password')"
                            />
                              <label for="photo">Photo</label>
                             <input
                                v-model="form.photo"
                                type="text"
                                name="photo"
                                placeholder="photo"
                                 class="form-control"
                            />
                            <div
                                v-if="form.errors.has('photo')"
                                v-html="form.errors.get('photo')"
                            />

                    </div>
                    <div class="modal-footer">
                                   <button  type="submit" class="btn btn-primary" >Add</button>

                    </div>
                    </form>
                </div>

            </div>

        </div>
        <!-- end modal -->
    </div>
</template>

<script>
export default {
    users : {},
    data: () => ({
        form: new Form({
            name: "",
            email: "",
            password: "",
            photo: ""
        })
    }),
    methods: {
    async addUser () {
      const response = await this.form.post('api/user')
      // ...
    }
  },
  created() {
      axios.get('api/user')
      .then(({data}) => (this.users = data.data));
  },
    mounted() {
        console.log("Component mounted.");
    }
};
</script>
