var imgSrc = []; //
var imgFile = []; //
var imgName = []; //

function imgUpload(obj) {
	var oInput = '#' + obj.inputId;
	var imgBox = '#' + obj.imgBox;
	var btn = '#' + obj.buttonId;
	$(oInput).on("change", function () {
		var fileImg = $(oInput)[0];
		var fileList = fileImg.files;

		if (fileList.length > obj.num || (fileList.length + imgFile.length) > obj.num) {
			alert('Upload up to ' + obj.num + ' images');
		}

		for (var i = 0; i < fileList.length; i++) {
			var imgSrcI = getObjectURL(fileList[i]);
			imgName.push(fileList[i].name);
			var fileType = fileList[i].name.substring(fileList[i].name.lastIndexOf("."));
			fileType = fileType.toLowerCase();
			if (fileType === ".jpg" || fileType === ".jpeg" || fileType === ".png" || fileType === ".bmp" || fileType === ".gif") {
				if (fileList[i].size < 3145728) {
					if (imgSrc.length > 1) {
					} else {
						imgSrc.push(imgSrcI);
						imgFile.push(fileList[i]);
					}
				} else {
					alert("The image cannot be larger than 3M");
				}
			} else {
				alert("The format of the image is jpg,png,bmp or gif");
			}

		}
		addNewContent(imgBox);

		if (imgFile.length >= obj.num) {
			$("#img-line").css("display", "none");
		}
	});


	$("#content").keyup(function () {
		if ($("#content").val() === null || $("#content").val().trim() === "") {
			$("#content").css("border-top", " 1px solid red");
			$("#content").css("border-right", " 1px solid red");
			$("#content").css("border-left", " 1px solid red");

			$("#tsspan").css("border-bottom", " 1px solid red");
			$("#tsspan").css("border-right", " 1px solid red");
			$("#tsspan").css("border-left", " 1px solid red");

		} else if ($("#content").val().length > 600) {
			$("#content").css("border-top", " 1px solid red");
			$("#content").css("border-right", " 1px solid red");
			$("#content").css("border-left", " 1px solid red");

			$("#tsspan").css("border-bottom", " 1px solid red");
			$("#tsspan").css("border-right", " 1px solid red");
			$("#tsspan").css("border-left", " 1px solid red");
		} else {
			$("#content").css("border-top", " 1px solid #E5E5E5");
			$("#content").css("border-right", " 1px solid #E5E5E5");
			$("#content").css("border-left", " 1px solid #E5E5E5");
			$("#tsspan").css("border-bottom", " 1px solid #E5E5E5");
			$("#tsspan").css("border-right", " 1px solid #E5E5E5");
			$("#tsspan").css("border-left", " 1px solid #E5E5E5");
		}
	});

	$("#submitBtn").on('click', function () {
		if ($("#content").val() === null || $("#content").val().trim() === "") {
			$("#content").css("border-top", " 1px solid red");
			$("#content").css("border-right", " 1px solid red");
			$("#content").css("border-left", " 1px solid red");

			$("#tsspan").css("border-bottom", " 1px solid red");
			$("#tsspan").css("border-right", " 1px solid red");
			$("#tsspan").css("border-left", " 1px solid red");

			return;
		} else if ($("#content").val().length > 600) {
			$("#content").css("border-top", " 1px solid red");
			$("#content").css("border-right", " 1px solid red");
			$("#content").css("border-left", " 1px solid red");

			$("#tsspan").css("border-bottom", " 1px solid red");
			$("#tsspan").css("border-right", " 1px solid red");
			$("#tsspan").css("border-left", " 1px solid red");
			return;
		} else {
			$("#content").css("border-top", " 1px solid #E5E5E5");
			$("#content").css("border-right", " 1px solid #E5E5E5");
			$("#content").css("border-left", " 1px solid #E5E5E5");
			$("#tsspan").css("border-bottom", " 1px solid #E5E5E5");
			$("#tsspan").css("border-right", " 1px solid #E5E5E5");
			$("#tsspan").css("border-left", " 1px solid #E5E5E5");
		}

		var ph = $("#phone").val();
		if (!ph || ph.length < 4 || ph.length > 20) {
			$(".sgselect-div").css("border-color", "red");
			return;
		} else {
			$(".sgselect-div").css("border-color", "#E5E5E5");
		}

		if (!limitNum(obj.num)) {
			alert('Upload up to ' + obj.num + ' images');
			return;
		}
		//formDate
		var fd = new FormData();
		for (var i = 0; i < imgFile.length; i++) {
			fd.append(obj.data + "[]", imgFile[i]);
		}
		submitPicture(fd);
		return false;
	});
}
//show pictures
function addNewContent(obj) {
	$(imgBox).html("");
	let box = '';
	for (let a = 0; a < imgSrc.length; a++) {
		box += '<div class="imgContainer"><img title=' + imgName[a] + ' alt=' + imgName[a] + ' src=' + imgSrc[a] + ' ><p onclick="removeImg(this,' + a + ')" class="imgDelete">delete</p></div>';
	}
	$(obj).html(box);
}
//delete
function removeImg(obj, index) {
	imgSrc.splice(index, 1);
	imgFile.splice(index, 1);
	imgName.splice(index, 1);
	var boxId = "#" + $(obj).parent('.imgContainer').parent().attr("id");
	addNewContent(boxId);
	if (imgFile.length < 2) {
		$("#img-line").css("display", "inline-block");
	}
	$('#file').val('');
}
//limit
function limitNum(num) {
	if (!num) {
		return true;
	} else if (imgFile.length > num) {
		return false;
	} else {
		return true;
	}
}

var post_flag = false;
function submitPicture(data) {
	if (post_flag) return;
	post_flag = true;
	data.append('content', unescape($("#content").val()));
	data.append('phone', $("#phone").val());
	data.append('countryCode', $("#countryCode").val());
	data.append('lang', $("#localelang").val());
	data.append('os', "");
	data.append('version', "");
	data.append('formtk', $("#formtk").val());
	url = '/addSuggestion';
	if (url && data) {
		$.ajax({
			type: "post",
			url: url,
			async: true,
			data: data,
			processData: false,
			dataType: "json",
			contentType: false,
			success: function (dat) {
				resetInputs();
				$("#sugok").show();
				$("body").css("overflow", "hidden");
				setTimeout(function () {
					$("#sugok").hide();
					$("body").css("overflow", "auto");
					$("#suggestad").toggle();
					$("#textCount").html(0);
					post_flag = false;
					window.location.reload();
				}, 3000);

			},
			error: function () {
				resetInputs();
				$("#sugok").show();
				$("body").css("overflow", "hidden");
				setTimeout(function () {
					$("#sugok").hide();
					$("body").css("overflow", "auto");
					$("#suggestad").toggle();
					$("#textCount").html(0);
					window.location.reload();
				}, 3000);

			}
		});
	}
}

function resetInputs() {
	$("#content").val('');
	$("#phone").val('');
	$("#countryCode").val('');
	$("#select").val($('#select option:first').val() || '');
	$("#file").val('');

	$(imgBox).html('');
	imgSrc.splice(0, imgSrc.length);
	imgFile.splice(0, imgFile.length);
	imgName.splice(0, imgName.length);
}

//
function imgDisplay(obj) {
	var src = $(obj).attr("src");
	var imgHtml = '<div style="width: 100%;height: 100vh;overflow: auto;background: rgba(0,0,0,0.5);text-align: center;position: fixed;top: 0;left: 0;z-index: 1000;"><img src=' + src + ' style="margin-top: 100px;width: 70%;margin-bottom: 100px;"/><p style="font-size: 50px;position: fixed;top: 30px;right: 30px;color: white;cursor: pointer;" onclick="closePicture(this)">×</p></div>';
	$('body').append(imgHtml);
}
//
function closePicture(obj) {
	$(obj).parent("div").remove();
}

//
function getObjectURL(file) {
	var url = null;
	if (window.createObjectURL != undefined) { // basic
		url = window.createObjectURL(file);
	} else if (window.URL != undefined) { // mozilla(firefox)
		url = window.URL.createObjectURL(file);
	} else if (window.webkitURL != undefined) { // webkit or chrome
		url = window.webkitURL.createObjectURL(file);
	}
	return url;
}
