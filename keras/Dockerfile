FROM qnstie/tf
LABEL maintainer "Pawel Kunstman <pawel@kunstman.net>"

RUN apt-get update && apt-get install -y \
	mc python3-tk graphviz \
	--no-install-recommends \
	&& rm -rf /var/lib/apt/lists/*

RUN pip install --upgrade pip

RUN pip install pydot graphviz imageio scikit-image

RUN pip install keras pydot

ENTRYPOINT [ "bash" ]
