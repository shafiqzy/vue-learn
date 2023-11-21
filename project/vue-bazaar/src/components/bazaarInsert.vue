<template>
    <div class="container">
        <div class="col">
            Bazaar Details
            <button class="btn btn-primary" data-toggle="modal" data-target="#insertModal"><i class="fa fa-plus"></i> Add</button>
            <!-- Modal -->
            <div class="modal fade" id="insertModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
                <div class="modal-dialog" role="document">
                    <div class="modal-content">
                    <div class="modal-header">
                        <h5 class="modal-title" id="exampleModalLabel">Insert Form</h5>
                        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                        <span aria-hidden="true">&times;</span>
                        </button>
                    </div>
                    <div class="modal-body">
                        <form><!--use .prevent so that the form does not reload-->
                            <div class="form-group">
                                <label for="Bname">Bazaar Name</label>
                                <input type="text" class="form-control" id="Bname" v-model="Bname">
                            </div>
                            <div class="form-group">
                                <label for="Bdescription">Bazaar Description</label>
                                <input type="text" class="form-control" id="Bdescription" v-model="Bdescription">
                            </div>
                            <div class="form-group">
                                <label for="Blocation">Bazaar location</label>
                                <input type="text" class="form-control" id="Blocation" v-model="Blocation">
                            </div>
                        </form>
                    </div>
                    <div class="modal-footer">
                        <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
                        <button type="button" class="btn btn-success" @click="bazaarInsert()"  data-dismiss="modal">Insert</button>
                    </div>
                    </div>
                </div>
            </div>
        </div>
        <div class="col col-md-auto">
            <div v-if="successMessage" class="alert alert-success">{{ successMessage }}</div>
        <div>
            <table class="table display " id="myTable">
                <thead class="table-secondary">
                    <tr>
                        <th>Bazaar Id</th>
                        <th>Bazaar Name</th>
                        <th>Bazaar Description</th>
                        <th>Bazaar Location</th>
                        <th colspan="2">Action</th>
                    </tr>
                </thead>
                

                <tr v-for="bz in bazaar" v-bind:key="bz.bazaarId">
                    <td>{{ bz.bazaarId }}</td>
                    <td>{{ bz.bazaarName }}</td>
                    <td>{{ bz.bazaarDescription }}</td>
                    <td>{{ bz.bazaarLocation }}</td>
                    <td><button class="btn btn-success" @click="updateModal = true ;bazaarEdit(bz.bazaarId)" data-toggle="modal" data-target="#updateModal"><i class="fa fa-book"></i> Edit</button></td>
                    <td><button class="btn btn-danger" @click="bazaarDel(bz.bazaarId)"><i class="fa fa-trash"></i> Delete</button></td>
                </tr>
            </table>
        </div>
            <!-- Modal -->
            <div class="modal fade" id="updateModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
            <div class="modal-dialog" role="document">
                <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title" id="exampleModalLabel">Insert Form</h5>
                    <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                    <span aria-hidden="true">&times;</span>
                    </button>
                </div>
                <div class="modal-body">
                    <form><!--use .prevent so that the form does not reload-->
                        <div class="form-group">
                            <label for="Bname">Bazaar Name</label>
                            <input type="hidden" class="form-control" id="Bname" v-model="form.bazaarId">
                            <input type="text" class="form-control" id="Bname" v-model="form.bazaarName">
                        </div>
                        <div class="form-group">
                            <label for="Bdescription">Bazaar Description</label>
                            <input type="text" class="form-control" id="Bdescription" v-model="form.bazaarDescription">
                        </div>
                        <div class="form-group">
                            <label for="Blocation">Bazaar location</label>
                            <input type="text" class="form-control" id="Blocation" v-model="form.bazaarLocation">
                        </div>
                    </form>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
                    <button type="button" class="btn btn-success" @click="submitForm()" data-dismiss="modal">Insert</button>
                </div>
                </div>
            </div>
        </div>
        </div>
        
    </div>
</template>
  
<script lang="ts">
import axios from 'axios'

export default {

    data() {
        return {
            Bname: '',
            Bdescription: '',
            Blocation: '',
            bazaar: [{
                bazaarId:'',
                bazaarName: '',
                bazaarDescription: '',
                bazaarLocation: '',
            }],
            successMessage:'',
            form: {
                bazaarId:'',
                bazaarName: '',
                bazaarDescription: '',
                bazaarLocation: ''
            },
            updateModal:false,
            showForm:false
        }
    },
    methods: {
        bazaarInsert() {

            axios.post(
                'http://localhost:3000/insertBazaar', {
                    //send data to api/db
                    Bname : this.Bname, Bdescription : this.Bdescription, Blocation : this.Blocation}
            ).then((response) => {
                console.log(response);
                this.updateModal = !this.updateModal;
                this.displayBazaar();
  

            })
        },

        submitForm(){

            axios.post(
                'http://localhost:3000/updateBazaar', {
                    //send data to api/db
                    bazaarId : this.form.bazaarId, bazaarName : this.form.bazaarName, bazaarDescription : this.form.bazaarDescription, bazaarLocation : this.form.bazaarLocation}
            ).then((response) => {
                console.log(response);
                this.displayBazaar();
            })
        },
        bazaarDel(id){
            console.log("Data: " , id);
            
            axios.post(
                'http://localhost:3000/delBazaar', {
                    //send data to api/db
                    bazaarId : id}
            ).then((response) => {
                console.log(response);
                if (response.status === 200) { // Check if the response was successful
                    this.successMessage = "Bazaar deleted successfully"; // Update a property to display message in the template
                }
            })  
        },
        bazaarEdit(id){

            axios.post(
                'http://localhost:3000/getBazaar', {
                    //send data to api/db
                    bazaarId : id}
                ).then(response => {
                    console.log(response.data);
                    this.showForm = !this.showForm;
                    
                    this.form.bazaarId = response.data.data[0].bazaarId
                    this.form.bazaarName = response.data.data[0].bazaarName
                    this.form.bazaarDescription = response.data.data[0].bazaarDescription
                    this.form.bazaarLocation = response.data.data[0].bazaarLocation
                } )
        },
        displayBazaar(){
            axios.post(
            'http://localhost:3000/listBazaar'
            )
        .then((response) => ( this.bazaar = response.data.data))
        }
        


    },
    mounted() {
        this.displayBazaar()
  }

}
</script>