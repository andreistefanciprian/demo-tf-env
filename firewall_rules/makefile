TF_DIR=tfcache
TF_EXEC=terraform
TF_BUCKET="$(GCP_PROJECT)-tfstate"
TF_VARFILE=tfvars.json
TF_PLANFILE="$(GCP_PROJECT).tfplan"

clean:
	@rm -rf .terraform
	@rm -Rf $(TF_DIR)

init: clean
	mkdir -p $(TF_DIR)    
	$(TF_EXEC) init \
	-no-color \
	-input=false \
	-backend-config="bucket=$(TF_BUCKET)" \
	-backend-config="prefix=terraform/firewall_rule" \
	$(TF_DIR)

plan: init
	$(TF_EXEC) plan -no-color -refresh=true -var-file=$(TF_VARFILE) -out $(TF_PLANFILE) $(TF_DIR)

apply:
	$(TF_EXEC) apply $(TF_PLANFILE) -no-color && rm $(TF_PLANFILE)

destroy: init
	$(TF_EXEC) destroy -no-color -input=false -auto-approve -var-file=$(TF_VARFILE) $(TF_DIR)