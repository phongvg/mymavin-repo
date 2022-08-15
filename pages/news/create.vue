<script>
import { FormWizard, TabContent, WizardButton } from "vue-form-wizard";
import vue2Dropzone from "vue2-dropzone";
import CKEditor from "@ckeditor/ckeditor5-vue";
import ClassicEditor from "@ckeditor/ckeditor5-build-classic";

import "vue-form-wizard/dist/vue-form-wizard.min.css";

/**
 * Product-create component
 */
export default {
  head() {
    return {
      title: `${this.title} | My Mavin`,
    };
  },
  components: {
    FormWizard,
    TabContent,
    WizardButton,
    vueDropzone: vue2Dropzone,
    ckeditor: CKEditor.component,
  },
  data() {
    return {
      title: "Tạo bài viết",
      items: [
        {
          text: "My Mavin",
        },
        {
          text: "Tin tức",
        },
        {
          text: "Tạo bài viết",
          active: true,
        },
      ],
      editor: ClassicEditor,
      editorData: "<p>...</p>",
      dropzoneOptions: {
        url: "https://httpbin.org/post",
        thumbnailWidth: 150,
        maxFilesize: 0.5,
        headers: {
          "My-Awesome-Header": "header value",
        },
        previewTemplate: this.template(),
      },
    };
  },
  methods: {
    template: function () {
      return ` <div class="dropzone-previews mt-3">
            <div class="card mt-1 mb-0 shadow-none border">
                <div class="p-2">
                    <div class="row align-items-center">
                        <div class="col-auto">
                            <img data-dz-thumbnail src="#" class="avatar-sm rounded bg-light" alt="">
                        </div>
                        <div class="col pl-0">
                            <a href="javascript:void(0);" class="text-muted font-weight-bold" data-dz-name></a>
                            <p class="mb-0" data-dz-size></p>
                        </div>
                        <div class="col-auto">
                            <!-- Button -->
                            <a href="" class="btn btn-link btn-lg text-muted" data-dz-remove>
                                <i class="fe-x"></i>
                            </a>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        `;
    },
    isLastStep() {
      if (this.$refs.wizard) {
        return this.$refs.wizard.isLastStep;
      }
      return false;
    },
  },
  middleware: "router-auth",
};
</script>

<template>
  <div>
    <PageHeader :title="title" :items="items" />

    <div class="row">
      <div class="col-lg-12">
        <div class="card">
          <div class="card-body">
            <form-wizard color="#00559a" ref="wizard">
              <h4 class="header-title">Thông tin chung</h4>
              <p class="sub-header">Những trường có dấu * là bắt buộc.</p>

              <div>
                <div class="row">
                  <div class="col-lg-6">
                    <div class="form-group mb-3">
                      <label for="product-name">
                        Tiêu đề bài viết
                        <span class="text-danger">*</span>
                      </label>
                      <input
                        type="text"
                        id="product-name"
                        class="form-control"
                      />
                    </div>
                  </div>
                  <div class="col-lg-6">
                    <div class="form-group mb-3">
                      <label for="product-category">
                        Loại tin tức
                        <span class="text-danger">*</span>
                      </label>
                      <select
                        class="form-control select2"
                        id="product-category"
                      >
                        <option>Lựa chọn</option>
                        <option value="SH1">Cấp tập đoàn</option>
                        <option value="SH2">Nội bộ cấp đơn vị</option>
                        <option value="SH3">Tin chính thống bên ngoài</option>
                      </select>
                    </div>
                  </div>
                </div>
                <div class="form-group mb-3">
                  <label for="product-description">
                    Nội dung
                    <span class="text-danger">*</span>
                  </label>
                  <ckeditor v-model="editorData" :editor="editor"></ckeditor>
                </div>

                <div class="row">
                  <div class="col-lg-6">
                    <div class="form-group mb-3">
                      <label for="product-summary">Nội dung tóm tắt</label>
                      <textarea
                        class="form-control"
                        id="product-summary"
                        rows="2"
                      ></textarea>
                    </div>
                  </div>
                  <div class="col-lg-6">
                    <div class="form-group mb-3">
                      <label for="product-category">
                        Chủ đề
                        <span class="text-danger">*</span>
                      </label>
                      <select
                        class="form-control select2"
                        id="product-category"
                      >
                        <option>Lựa chọn</option>
                        <optgroup label="Loại chủ đề 1">
                          <option value="SH1">Chủ đề 1</option>
                          <option value="SH2">Chủ đề 2</option>
                          <option value="SH3">Chủ đề 3</option>
                          <option value="SH4">Chủ đề 4</option>
                        </optgroup>
                        <optgroup label="Loại chủ đề 2">
                          <option value="SH1">Chủ đề 1</option>
                          <option value="SH2">Chủ đề 2</option>
                          <option value="SH3">Chủ đề 3</option>
                          <option value="SH4">Chủ đề 4</option>
                        </optgroup>
                      </select>
                    </div>
                  </div>
                </div>
                <!-- <div class="form-group mb-0">
                  <label>Comment</label>
                  <textarea
                    class="form-control"
                    rows="3"
                    placeholder="Please enter comment"
                  ></textarea>
                </div> -->
              </div>

              <ul class="pager wizard mb-0 list-inline text-right mt-3">
                <li class="next list-inline-item"></li>
              </ul>

              <h4 class="header-title">Ảnh chủ đề bài viết</h4>
              <p class="sub-header">Tải ảnh lên</p>

              <vue-dropzone
                id="dropzone"
                ref="myVueDropzone"
                :use-custom-slot="true"
                :options="dropzoneOptions"
              >
                <div class="dz-message needsclick">
                  <i class="h1 text-muted ri-upload-cloud-2-line"></i>
                  <h3>Kéo ảnh vào hoặc bấm vào đây để tải ảnh lên.</h3>
                  <span class="text-muted font-13">
                    (This is just a demo dropzone. Selected files are
                    <strong>not</strong> actually uploaded.)
                  </span>
                </div>
              </vue-dropzone>

              <!-- <h4 class="header-title">Meta Data</h4>
              <p class="sub-header">Fill all information below</p>

              <form>
                <div class="form-group mb-3">
                  <label for="product-meta-title">Meta title</label>
                  <input
                    type="text"
                    class="form-control"
                    id="product-meta-title"
                    placeholder="Enter title"
                  />
                </div>

                <div class="form-group mb-3">
                  <label for="product-meta-keywords">Meta Keywords</label>
                  <input
                    type="text"
                    class="form-control"
                    id="product-meta-keywords"
                    placeholder="Enter keywords"
                  />
                </div>

                <div class="form-group mb-0">
                  <label for="product-meta-description">Meta Description</label>
                  <textarea
                    class="form-control"
                    rows="5"
                    id="product-meta-description"
                    placeholder="Please enter description"
                  ></textarea>
                </div>
              </form> -->
            </form-wizard>
          </div>
        </div>
      </div>
    </div>
    <!-- end row -->
  </div>
</template>
